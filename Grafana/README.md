## Install Grafana
#### Grafana is an excellent solution for effectively monitoring the performance and health of your server systems. Today, I am bringing you a guide on how to install a Grafana server in a few very simple steps.

```
sudo apt install grafana -y
```
```
sudo systemctl enable --now grafana-server
```
```
http://<your-ip>:3000
```
## Create Your Accont in Grafana

## Before the adding datasourse you should configure Loki and Prometheus on same Server or same VM 

#### Click the Connections on the left menu, then select Data Sources.
- Click Add data source and select Prometheus.
  Set the URL to http://localhost:9090 and click Save & Test.
  
- Go back, click Add data source again, and select Loki.
  Set the URL to http://localhost:3100 and click Save & Test.
