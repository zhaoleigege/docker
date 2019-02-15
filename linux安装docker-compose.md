# linux安装docker-compose

1. 下载离线文件

   ```shell
   # 具体的版本信息查看[官网](https://github.com/docker/compose/releases)
   sudo curl -L "https://github.com/docker/compose/releases/download/1.23.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
   ```

2. 添加执行权限

   ```shell
   sudo chmod +x /usr/local/bin/docker-compose
   ```

3. 查看是否安装成功

   ```shell
   docker-compose --version
   ```






#### 参考资料

* [Install Docker Compose](https://docs.docker.com/compose/install/)