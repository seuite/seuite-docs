# 基本组件设置

## 一行代码登录SEU-Wlan
curl -3 'https://w.seu.edu.cn/portal/login.php' -d 'username=your_username' -d 'password=your_password'

## Nginx
Set Nginx Installed by a Prebuilt CentOS/RHEL Package from the OS Repository
```
$ sudo yum install epel-release
```

Update the repository:
```
$ sudo yum update -y
```

Install NGINX Open Source:
```
$ sudo yum install nginx
```

Verify the installation:
```
$ sudo nginx -v
nginx version: nginx/1.6.3
```

Create the user nginx for Nginx running:
```
$ sudo groupadd www 
$ sudo useradd -g www nginx
```

Check the conf is whether right
```
$ nginx -t
```

Start the Nginx
```
$ service nginx start
```

### Nginx容器
重载配置
```
docker exec -it nginx /etc/init.d/nginx reload
```

## Docker
### Docker安装
使用阿里云镜像加速，阿里云镜像每十分钟与docker官方镜像进行同步（2019-3-20）
```
sudo curl -fsSL https://get.docker.com | bash -s docker --mirror Aliyun
```
建议一同安装docker-compose
```
sudo curl -L "https://github.com/docker/compose/releases/download/1.23.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
```
**注意：** 此处安装的docker和docker-compose使用的1.23.2版本均乃官方截止2019-3-20的最新版本，请阅读官方文档以确定你所应安装的docker-compose版本
- [Docker](https://docs.docker.com/install/)
- [Docker-Compose](https://docs.docker.com/compose/install/)

启动docker服务
```
sudo systemctl start docker
```

加载一个hello-world容器来确认docker正常安装
```
sudo docker run hello-world
```

### Docker加速
这里使用了我在阿里云上注册的docker加速器
```
sudo mkdir -p /etc/docker
sudo tee /etc/docker/daemon.json <<-'EOF'
{
  "registry-mirrors": ["https://v8thd0yh.mirror.aliyuncs.com"]
}
EOF
sudo systemctl daemon-reload
sudo systemctl restart docker
```

### 查找容器内的用户名及密码
```bash
$ docker logs <容器名orID> 2>&1 | grep '^User: ' | tail -n1
```

## 安装系统监视器 netdata
```
docker run -d --name=netdata \
  -p 19999:19999 \
  -v /proc:/host/proc:ro \
  -v /sys:/host/sys:ro \
  -v /var/run/docker.sock:/var/run/docker.sock:ro \
  --cap-add SYS_PTRACE \
  --security-opt apparmor=unconfined \
  netdata/netdata
```