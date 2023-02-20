# 部署documentserver

* 拉取镜像

  ``` shell
  docker pull onlyoffice/documentserver
  ```

* 运行镜像

  * 创建数据目录

    ```shell
    # 创建对应目录
    mkdir logs
    mkdir data
    mkdir lib
    mkdir db
    ```

  * 启动docker容器

    ```shell
    docker run --name onlyoffice -i -t -d -e TZ="Asia/Shanghai" -p 8000:80 --restart=always -v E:/docker/onlyoffice/logs:/var/log/onlyoffice -v E:/docker/onlyoffice/data:/var/www/onlyoffice/Data -v E:/docker/onlyoffice/lib:/var/lib/onlyoffice -v E:/docker/onlyoffice/db:/var/lib/postgresql -v E:/docker/onlyoffice/local.json:/etc/onlyoffice/documentserver/local.json onlyoffice/documentserver
    ```

    