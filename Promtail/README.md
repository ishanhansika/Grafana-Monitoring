## Promtail

<img width="502" height="221" alt="image" src="https://github.com/user-attachments/assets/931e0b88-96d2-4c09-bf70-2ad9f50d9e37" />

#### Install Promtail (Log Collector)
```
cd /usr/local/bin
```
```
sudo wget https://github.com/grafana/loki/releases/latest/download/promtail-linux-amd64.zip
```

#### executable permission
```
sudo unzip promtail-linux-amd64.zip
```
```
sudo chmod +x promtail-linux-amd64
```
```
sudo mv promtail-linux-amd64 promtail
```

#### Create Promtail Configuration File
```
sudo nano /etc/loki/promtail-config.yml
```
```
server:

  http_listen_port: 9080


positions:

  filename: /var/lib/promtail/positions.yaml


clients:

  - url: http://localhost:3100/loki/api/v1/push   #you need to put the ip address of the server where you have installed loki


scrape_configs:

  - job_name: system

    static_configs:

      - targets:

          - localhost

        labels:

          job: syslog

          host: NewServerName    # server name  

          __path__: /var/log/*.log
```

#### Create the directory
```
sudo mkdir -p /var/lib/promtail
```

#### Create Promtail systemd Service
```
sudo nano /etc/systemd/system/promtail.service
```
```
[Unit]

Description=Promtail Log Collector

After=network.target


[Service]

ExecStart=/usr/local/bin/promtail -config.file=/etc/loki/promtail-config.yml

Restart=always

User=root


[Install]

WantedBy=multi-user.target
```

#### Enable and start
```
sudo systemctl daemon-reload
```
```
sudo systemctl start promtail
```
```
sudo systemctl enable promtail
```

#### Check status
```
sudo systemctl status promtail
```

