
# 如何搭建一个镜像站

## 1. 硬件环境
服务器推荐硬件参数如下：
>    CPU: 8 核心 2.5GHz 以上
>
>    内存: 32 GB 以上
>
>    硬盘: 2TB 以上
>
>    网络: 百兆上行带宽及以上

作为参考，本镜像站已用硬盘容量为
- CentOS 139G
- EPEL 193.33G
- Ubuntu 1.30T

## 2. 同步源
从官方源中选择支持rsync的国内镜像源同步

Ubuntu 源列表：https://launchpad.net/ubuntu/+archivemirrors
```
rsync://mirrors.shuosc.org/ubuntu/
rsync://mirrors.sohu.com/ubuntu/
rsync://mirrors.tuna.tsinghua.edu.cn/ubuntu/
rsync://mirrors.ustc.edu.cn/ubuntu/
rsync://mirrors.yun-idc.com/ubuntu/
```

CentOS 源列表：https://www.centos.org/download/mirrors/
```
rsync://mirrors.tuna.tsinghua.edu.cn/centos/
rsync://mirror.es.its.nyu.edu/centos/
rsync://centos.sonn.com/CentOS/
```

EPEL 源列表：https://admin.fedoraproject.org/mirrormanager/mirrors/EPEL
```
rsync://mirrors.yun-idc.com/epel
rsync://rsync.mirrors.ustc.edu.cn/epel
```

## 3. 同步架构
使用rsync做增量同步，实际使用Tuna的开源项目tunasync的预编译版本v0.3.3

## 4. 系统配置
创建用户及用户组
```bash
sudo groupadd -g 2001 mirrorgroup
sudo useradd -u 2101 -g mirrorgroup mirrors
sudo passwd mirrors
```

建立应用及数据目录
```bash
mkdir /home/mirrors/tunasync
mkdir /home/mirrors/tunasync/conf
mkdir /home/mirrors/tunasync/db
```

建立镜像数据目录
```bash
mkdir /mirrors
```

修改数据目录用户
```bash
sudo chown -R mirrors:mirrorgroup /mirrors /home/mirrors/tunasync /home/mirrors/tunasync/conf /home/mirrors/tunasync/db
```

切换到mirrors用户
```bash
su mirrors
```

## 5. 同步配置文件
tunasync分为同步服务端和同步客户端，本镜像站为便于管理，均统一放置在`/home/mirrors/tunasync/conf/`目录下

### manager配置(manager.conf)
```
debug = false

[server]
addr = "127.0.0.1"
port = 14242
ssl_cert = ""
ssl_key = ""

[files]
db_type = "bolt"
db_file = "/home/mirrors/tunasync/db/manager.db"
ca_cert = ""
```
- port：监听端口，同客户端同步（在预编译版本中需固定配置为14242）
- ssl设置：在localhost中可不用配置，若需要配置分布式服务器建议配置
- db_file：数据库文件，统一置于`/home/mirrors/tunasync/db/`目录

### worker配置(worker-'$workername'.conf)
```
[global]
name = "some worker"
log_dir = "/home/mirrors/log/tunasync/{{.Name}}"
mirror_dir = "/home/mirrors"
concurrent = 10
interval = 1440

[manager]
api_base = "http://localhost:14242"
token = "some_token"
ca_cert = ""

[cgroup]
enable = false
base_path = "/sys/fs/cgroup"
group = "tunasync"

[server]
hostname = "localhost"
listen_addr = "127.0.0.1"
listen_port = 16010
ssl_cert = ""
ssl_key = ""

[[mirrors]]
name = "centos"
provider = "rsync"
upstream = "rsync://examle.com/mirrors"
use_ipv6 = false
```
- [global]
    - name: worker 进程名称，用于程序识别
    - log_dir：本进程的tunasync日志路径
    - mirror_dir：镜像下载地址
    - concurrent：并发线程数
    - interval：rsync的同步周期，以分钟为单位
- [manager]（均需与manager中保持一致）
    - api_base：manager地址（含端口）
    - token：认证口令
    - ca_cert：CA证书
- [server] 
    - listen_port：该worker自身的监听端口，**如果一台服务器上有多个不同的worker，需保证各个worker的监听端口互不相同**
- [mirrors]
    - name：镜像名称，tunasync会在根镜像目录下建立一个该名称的目录用于下载镜像
    - provider：上游源使用协议，推荐rsync
    - upstream：同步地址，注意，参数最后需要以'/'结束，否则tunasync不能正确识别地址
    - use_ipv6：是否使用ipv6

## 6. 启动同步应用
启动 tunasync 需开启 manager 进程与 worker 进程，先启动 manager，后启动 worker。为了便于监控系统进程情况，建立 /mirrors/log/plog/ 目录，所有进程的工作日志在该目录中（注意，此处日志为系统终端输出日志，与 tunasync 自身工作日志不同）。以下命令由 mirrors 用户操作
- 检查环境
```
cd /home/mirrors/tunasync
su root
chmod +x tunasync tunasynctl
su mirrors
```
- 启动manager服务（后台进程）：
```
./tunasync manager --config /home/mirrors/tunasync/conf/manager.conf >> /home/mirrors/log/mirrorlog/manager.log &
```
- 开启 worker 服务（根据需要同步的镜像开启，替换'$workername'为你需要的镜像）：
```
./tunasync worker --config /home/mirrors/tunasync/conf/worker-'$workername'.conf >> /home/mirrors/log/mirrorlog/worker-'$workername'.log &
```
此时镜像就已经开始从上游源同步下来了

## 7. 运行维护
tunasync同时提供了管理工具tunasynctl，可以用于对镜像服务做一些管理
- 更新镜像信息
```
./tunasynctl set-size -w <worker-id> <mirror> <size>
```
- 获取任务状态信息并保存为json文件
```
wget -c http://localhost:14242/jobs -O /mirrors/jobs.json -o /mirrors/log/plog/wget.log
```
以上任务可以整合为crontab定时任务，并同步到 web 前端页面中。

- 删除worker进程
```
tunasynctl rm-worker -w <worker-id>
```

## 提供服务

### rsync
**不推荐小型镜像站开放rsync服务**

rsync的io负载较大，建议配置好多级缓存后再开启

### ftp
**推荐使用sftp或ftps**

### sftp
sftp服务内建于ssh服务内，因此只需创建一个不可登陆命令行的低权限用户，分配合适的文件夹下合适的权限，并开启ssh-server即可

### ftps
本站出于安全，效率和配置难度考虑，使用vsftpd提供服务
***
待填充配置文件
***

## http(s)
由于本站同时提供其它[seu.services](https://www.seu.services)服务，故继续使用Nginx作为WebServer

首先应安装好nginx并正确初始化，我们推荐两种方式
- Docker安装，请参考[全站容器化](https://docs.seu.services/guide/dockerbasic)中的[Nginx部分](https://docs.seu.services/guide/DockerBasic#Nginx)
- 直接安装，请参考[基本组件配置](https://docs.seu.services/guide/BasicComponents)中的[Nginx部分](https://docs.seu.services/guide/BasicComponents#Nginx)

安装完成后，在nginx配置目录(默认为 `/etc/nginx/conf.d` )下创建 `mirrors.conf` 文件，参考我们的[nginx配置文件](https://docs.seu.services/guide/nginxconf)进行编辑，然后用合适的用户运行
```bash
nginx -t #检查配置文件正确性
nginx -s reload #重新加载nginx配置文件
```
你的镜像站已经准备就绪，继续你的旅途吧！

## 附录：加入官方Mirror List教程
各上游源要求不同，请到相关页面确认

## 成为CentOS注册公开源之一
- 地址：<https://wiki.centos.org/HowTos/CreatePublicMirrors>
- 要求：
    1. 硬盘容量不小于15Tb
    2. 带宽高于100Mbit/s
- 步骤：
    1. 加入Mailing List：[CentOS-mirror mailing list](https://lists.centos.org/mailman/listinfo/CentOS-mirror) (一般镜像) 或 [CentOS-mirror-announce mailing list](https://lists.centos.org/mailman/listinfo/centos-mirror-announce)(低带宽，定制化和非官方分支)
    2. 将镜像同步至[官方版本](https://lists.centos.org/mailman/listinfo/centos-mirror-announce)
    3. 保证你的镜像站能够正确和稳定的工作并提供**HTTPS**和**RSYNC**服务，HTTP已逐渐**不再接受**申请，如果你的镜像站能够同时提供ipv4和ipv6，请分别提供两个服务
    4. 按照如下邮件格式给centos-mirror list，当检查通过后，你的镜像站就会成为官方注册公开源之一
    ```
    HTTP: http://your.domain.com/centos/ 
    HTTPS: https://your.domain.com/centos/ (if you provide https access)
    RSYNC: rsync://your.domain.com/centos/ (if you provide rsync access)

    Sync schedule: Every x hrs
    Bandwidth: 
    Location: (For U.S. and Canada: also mention the state/province)
    Sponsor: 
    Sponsor URL:
    IPv4 address to authorize: 
    IPv6 address to authorize: 
    Email contact: (where we'll send notifications for issues with your mirror)
    Mirroring AltArch: yes/no (and if so, let us know the URLs, as those will be different from your http/https/rsync paths for CentOS)
    ```

## 成为Ubuntu注册公开源之一
1. [注册](https://login.launchpad.net/jA7wF593j5xIkpxQ/+decide)
2. 填写资料
3. 等待认证

恭喜你，你成为Ubuntu官方注册公开源之一啦

## Reference & 致谢
1. [清华大学开源软件镜像站](https://mirrors.tuna.tsinghua.edu.cn/)
2. [搭建开源软件镜像站 (中山大学)](https://fangpeishi.com/build_opensource_mirror.html)
3. 看到现在的你

![Susan](https://i.loli.net/2019/03/21/5c93ac20dc3f5.png) 