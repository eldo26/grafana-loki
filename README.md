# grafana-loki

### config files
```
wget https://raw.githubusercontent.com/grafana/loki/v2.9.2/cmd/loki/loki-local-config.yaml -O loki-config.yaml
wget https://raw.githubusercontent.com/grafana/loki/v2.9.2/clients/cmd/promtail/promtail-docker-config.yaml -O promtail-config.yaml
```


### commands
```
docker run -d --net mylab --name=grafana -p 3000:3000 grafana/grafana
docker run -d -p 9090:80 -v $(pwd)/data/nginx_1:/var/log/nginx --name nginx1 nginx_demo:v1
docker run -d -p 9091:80 -v $(pwd)/data/nginx_2:/var/log/nginx --name nginx2 nginx_demo:v1
docker run --net mylab --name loki -d -v $(pwd):/mnt/config -p 3100:3100 grafana/loki:2.9.2 -config.file=/mnt/config/loki-config.yaml
docker run --net mylab --name promtail -d -v $(pwd):/mnt/config -v $(pwd)/data:/data --link loki grafana/promtail:2.9.2 -config.file=/mnt/config/promtail-config.yaml
```
