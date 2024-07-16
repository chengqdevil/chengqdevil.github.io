`watchtower`可以定期检查本地所有的`docker`容器，当它们存在新版本时，自动进行更新。
检查更新本地所有的`docker`容器，并在更新后自动清理旧版本的镜像
```
docker run --rm --name watchtower -e TZ=Asia/Shanghai -v /var/run/docker.sock:/var/run/docker.sock containrrr/watchtower:latest --cleanup --run-once
```
检查更新指定容器，并在更新后自动清理旧版本的镜像，只需要在命令后面加上容器名称，例如`vaultwarden`和`nginx`
```
docker run --rm --name watchtower -e TZ=Asia/Shanghai -v /var/run/docker.sock:/var/run/docker.sock containrrr/watchtower:latest --cleanup --run-once vaultwarden nginx
```
通过`Portainer`创建一个`持续运行`的`watchtower`容器来定期检查更新所有容器
```
version: "3"

services:
 watchtower:
   image: containrrr/watchtower:latest
   restart: always
   environment:
     TZ: Asia/Shanghai                               # 容器内部时区
     WATCHTOWER_CLEANUP: "true"
     WATCHTOWER_POLL_INTERVAL: 7200 # 每 2 小时检查更新一次
   volumes:
     - "/var/run/docker.sock:/var/run/docker.sock"
   # command: vaultwarden nginx 检查更新指定容器
```

<!-- ##{"timestamp":1667360280}## -->