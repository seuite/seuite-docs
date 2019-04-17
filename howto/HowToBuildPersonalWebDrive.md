# 如何搭建个人/小型团队网盘

## TL;DR

> 有现成的别自己折腾

## WebDav

1. 配置好基础环境：Nginx
2. 使用提供的 DefaultWebDavServer.conf
3. 导入密码，有两种方式
   1. 在[这里](http://tool.oschina.net/htpasswd)自动生成密码后导入上面的.passwords.list
   2. 使用命令行直接创建

    ```bash
    # 创建新用户
    $ echo -n 'username:' | sudo tee /etc/nginx/.passwords.list
    # 设定用户密码
    $ openssl passwd -apr1 | sudo tee -a /etc/nginx/.passwords.list
    Password: # 输入用户的密码
    ```
4. 配置好客户端即可

## h5ai

1. 配置好基础环境：Docker
2. 运行
    ```bash
    docker run -d -p $Your_port:80 -v $PWD:/h5ai --name h5ai ilemonrain/h5ai:full #https://blog.ilemonrain.com/docker/h5ai.html
    ```
3. 访问你配置好的端口即可