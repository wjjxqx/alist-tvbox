# alist-tvbox GHCR 镜像部署说明


docker run -d -p 4566:4567 --restart=always --name=alist-tvbox \
  -v /opt/xiaoya:/www/static \
  -v /opt/xiaoya:/opt/alist/data \
  -v /opt/xiaoya:/www \
  ghcr.io/wjjxqx/alist-tvbox:latest

docker pull ghcr.io/wjjxqx/alist-tvbox:latest

docker run -d \
-p 4566:4567 \
--restart=always \
--name=alist-tvbox \
-v /opt/xiaoya:/www/static \
-v /opt/xiaoya:/opt/alist/data \
-v /opt/xiaoya:/www \
ghcr.io/wjjxqx/alist-tvbox:latest

查看密码：
docker exec -it alist-tvbox cat /data/initial_admin_credentials.txt




## 1. 镜像地址

```
ghcr.io/wjjxqx/alist-tvbox:latest
ghcr.io/wjjxqx/alist-tvbox:<tag>
```

示例：
```
ghcr.io/wjjxqx/alist-tvbox:1.91.0
ghcr.io/wjjxqx/alist-tvbox:latest
```

## 2. 前提条件

- OpenWrt 已安装 Docker 和 Docker Compose
- 网络可访问 `ghcr.io`
- 端口 `4566`（或自定义）未被占用

## 3. 快速启动

```bash
docker run -d \
  --name atv \
  --restart always \
  -p 4566:4566 \
  -v /opt/atv/data:/www/static \
  ghcr.io/wjjxqx/alist-tvbox:latest
```

## 4. Docker Compose 示例

```yaml
version: "3"
services:
  alist-tvbox:
    image: ghcr.io/wjjxqx/alist-tvbox:latest
    container_name: atv
    restart: always
    ports:
      - "4566:4566"
    volumes:
      - /opt/atv/data:/www/static
```

## 5. 验证

```bash
curl http://localhost:4566/api/alist/status
# 返回 2 表示运行正常
```

## 6. 更新

```bash
docker compose pull
docker compose up -d --force-recreate
```
