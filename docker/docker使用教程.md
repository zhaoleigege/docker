# Docker使用教程

1. linux下载docker

   ```shell
   
   ```

2. 设置管理docker不需要root权限

   ```shell
   sudo groupadd docker
   sudo usermod -aG docker $USER
   # 退出登录然后登入
   ```

3. docker搭建自己的私有仓库

   1. docker私有服务器配置

      ```shell
      # 启动docker仓库
      docker run -d -p 5000:5000 --restart=always --name registry -v /home/coreos/registry:/var/lib/registry registry:2
      ```

      重启docker

      ```shell
      sudo  systemctl restart  docker
      ```

   2. docker客户端配置

      ```shell
      # 在需要上传镜像到docker仓库的服务器的主机上配置docker的相关信息
      # 在/etc/docker/daemon.json文件中添加如下信息
      "insecure-registries" : [
          "192.168.124.72:5000"   # docker仓库的信息
        ]
      ```

   3. 测试

      ```shell
      # 生成一个image
      docker tag nginx:latest 192.168.124.72:5000/nginx
      
      # 推送到服务端
      docker push 192.168.124.72:5000/nginx
      ```

      服务端查看有哪些镜像

      ```shell
      curl http://192.168.124.72:5000/v2/_catalog
      ```


#### 参考资料

* [Docker 入门教程](http://www.ruanyifeng.com/blog/2018/02/docker-tutorial.html)
* [Docker 微服务教程](http://www.ruanyifeng.com/blog/2018/02/docker-wordpress-tutorial.html)
* [配置docker私有仓库出现访问错误的问题](./Running%20a%20remote%20Docker%20Registry%20and%20getting%20%E2%80%98HTTP%20response%20to%20HTTPS%20request%E2%80%99%20error%20on%20push/Running-a-remote-Docker-Registry-and-getting-%E2%80%98HTTP-response-to-HTTPS-request%E2%80%99-error-on-push-%E2%80%93-Kev's-Development-Toolbox.html)

