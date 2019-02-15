# docker绿色版安装

1. 前往[docker官方源](https://download.docker.com/linux/static/stable/)下载安装docker二进制版本，下载的包为压缩包形式

   ```shell
   # 解压压缩包
   tar xzvf docker-18.09.1.tgz 
   # 拷贝生成的文件到相应目录中
   sudo cp docker/* /usr/bin/ 
   ```

2. 设置docker使用systemd进行管理

   1. 拷贝该[网站](https://github.com/moby/moby/tree/master/contrib/init/systemd)的文件到本地

      ```shell
      docker.socket
      docker.service
      ```

   2. 拷贝`docker.service`和`docker.socket`文件到`/etc/systemd/system`目录下

      ```shell
      sudo cp docker.socket /etc/systemd/system
      sudo cp docker.service /etc/systemd/system
      ```

   3. 使得配置文件生效

      ```shell
      # 重启systemctl服务
      sudo systemctl daemon-reload
      # 重启电脑
      sudo reboot
      ```

      ```shell
      # 再次开启docker服务
      sudo systemctl start docker
      
      # 配置docker开机自启动
      sudo systemctl enable docker
      ```

3. 设置docker命令不需要root权限

   ```shell
   sudo groupadd docker
   sudo usermod -aG docker $USER
   # 重启生效
   ```

4. [阿里云镜像加速](https://cr.console.aliyun.com/)

   ```shell
   # 前往网站
   https://cr.console.aliyun.com/
   # 点击左侧的镜像加速，复制
   # {"registry-mirrors": [...]}
   
   # 本地编写配置文件
   sudo vim /etc/docker/daemon.json
   # 粘贴刚刚的内容进去
   
   # 重启生效
   sudo systemctl daemon-reload
   sudo systemctl restart docker
   ```

5. 测试安装成功

   ```shell
   docker run hello-world
   ```

