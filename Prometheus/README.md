## Prometheus
#### Core Communication Details
<center><img width="543" height="467" alt="image" src="https://github.com/user-attachments/assets/a3c3cac7-a72a-4c53-a181-2193a2a864de" /></center>


#### Install Prometheus
```
apt -y install prometheus-node-exporter
```

#### Edit the Configuration File Add Remote Nodes
```
nano /etc/prometheus/prometheus.yml
```
```
- job_name: Monitoring Server
    static_configs:
      - targets: ['node01.srv.world:9100']    #youneed to change this here.you need to put the ip of the server you want to monitor.
```

#### Start and Enable Prometheus
```
sudo systemctl daemon-reload
```
```
sudo systemctl start prometheus
```
```
sudo systemctl enable prometheus
```

#### Open the Browser and go to the site
```
http://(Prometheus server's hostname or IP address):9090
```

