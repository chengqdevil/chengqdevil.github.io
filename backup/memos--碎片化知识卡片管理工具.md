[Memos](https://github.com/usememos/memos)：一个开源的、支持私有化部署的`碎片化知识卡片`管理工具。
```
mkdir -p /volume1/docker/memos
```
```
docker run -d \
  --restart=always \
  --name="memos" \
  -p 5230:5230 \
  -v /volume1/docker/memos:/var/opt/memos \
  -e mode=prod \
  -e TZ=Asia/Shanghai \
  neosmemo/memos:latest \
```

<!-- ##{"timestamp":1667350863}## -->