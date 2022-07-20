# 在 docker-compose 上使用 Let's Encrypt 的 nginx 样板



使用 nginx 的 docker-compose 设置中获取并确保更新一个或多个域的 Let's Encrypt 证书。当您需要将 nginx 设置为应用程序的反向代理时，这很有用。

## 安装

1. [安装 docker-compose](https://docs.docker.com/compose/install/#install-compose)。
2. 克隆此存储库：`git clone https://github.com/hjue/nginx-certbot.git .`
3. 修改配置：

- 将域和电子邮件地址添加到 compose.yml
- 运行初始化脚本：

```
docker-compose up -d webserver
```

4. 获取证书

```
docker-compose up -d certbot
```

5. 修改samples/site.conf 中的域名，替换 nginx/conf/site.conf

```
cp samples/site.conf nginx/conf/site.conf
```



5. 重启nginx 服务

```
 docker-compose restart
```



## 自动 renew 证书

配置 crontab，每月 1 号早上 5 点更新证书



```
0 5 1 * *  /usr/local/bin/docker-compose up -f /var/docker/compose.yml certbot
```

