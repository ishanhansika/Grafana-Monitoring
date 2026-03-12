## Node Exporter 

#### Install and Configure Node Exporter
```
wget https://github.com/prometheus/node_exporter/releases/download/v1.9.0/node_exporter-1.9.0.linux-amd64.tar.gz
```

#### Extract and Move the Binary
```
tar -xvf node_exporter-1.9.0.linux-amd64.tar.gz
```
```
sudo mv node_exporter-1.9.0.linux-amd64/node_exporter /usr/local/bin/
```

#### Create a System User
```
sudo useradd --system --no-create-home --shell /bin/false node_exporter
```

#### Set Up Node Exporter as a Service
```
sudo nano /etc/systemd/system/node_exporter.service
```
```
[Unit]
Description=Node Exporter
After=network.target
Wants=network-online.target

[Service]
User=node_exporter
Group=node_exporter
Type=simple

ExecStart=/usr/local/bin/node_exporter

# Securtiy Settings
ProtectHome=true
NoNewPrivileges=true
ProtectSystem=strict
PrivateTmp=true
PrivateDevices=true
ProtectKernelTunables=true
ProtectKernelModules=true
ProtectControlGroups=true
RestrictNamespaces=true
RestrictRealtime=true
RestrictSUIDSGID=true

# Resources
LimitNPROC=8192
LimitNOFILE=65535
LimitCORE=infinity

# Restart
Restart=always
RestartSec=5

[Install]
WantedBy=multi-user.target
```
#### Start and Enable Node Exporter
```
sudo systemctl daemon-reload
```
```
sudo systemctl start node_exporter
```
```
sudo systemctl enable node_exporter
```
#### Verify Node Exporter
```
 ss -aplnt | grep 9100
```
```
curl http://localhost:9100/metrics
```
