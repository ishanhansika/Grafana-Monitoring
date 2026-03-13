## Loki

#### Create a Dedicated Loki Directory
```
sudo mkdir -p /etc/loki /var/lib/loki
```
#### Download Loki Binary
```
cd /usr/local/bin
```
```
sudo wget https://github.com/grafana/loki/releases/latest/download/loki-linux-amd64.zip
```
#### Get the executable permissions:
```
sudo unzip loki-linux-amd64.zip
```
```
sudo chmod +x loki-linux-amd64
```
```
sudo mv loki-linux-amd64 loki
```
Loki is ready to go.

#### Create Loki Configuration File
```
sudo nano /etc/loki/loki-config.yml
```
```

auth_enabled: false


server:

  http_listen_port: 3100


ingester:

  lifecycler:

    address: 127.0.0.1

    ring:

      kvstore:

        store: inmemory

      replication_factor: 1

  chunk_idle_period: 3m

  chunk_retain_period: 1m


schema_config:

  configs:

  - from: 2020-10-24

    store: boltdb

    object_store: filesystem

    schema: v11

    index:

      prefix: index_

      period: 24h


storage_config:

  boltdb:

    directory: /var/lib/loki/index


  filesystem:

    directory: /var/lib/loki/chunks


limits_config:

  ingestion_rate_mb: 4

  max_cache_freshness_per_query: 10m

```

#### Create Loki systemd Service
```
sudo nano /etc/systemd/system/loki.service
```
Add:
```
[Unit]

Description=Loki Log Aggregation System

After=network.target


[Service]

ExecStart=/usr/local/bin/loki -config.file=/etc/loki/loki-config.yml

Restart=always

User=root


[Install]

WantedBy=multi-user.target
```

#### Reload the system
```
sudo systemctl daemon-reload
```
```
sudo systemctl start loki
```
```
sudo systemctl enable loki
```


