# Monitoring Install Guide - Linux

## Installing Node Exporter
Node Exporter pushes statistics on CPU, RAM, Network traffic, processes and disk I/O to port 9182. When running, you can see the metrics by going to http://localhost:9182/statistics

**Step 1:** Download the latest version of node exporter. Check [Prometheus download section](https://prometheus.io/download/) for the newest package:

    cd /tmp
    curl -LO https://github.com/prometheus/node_exporter/releases/download/v1.0.1/node_exporter-1.0.1.linux-amd64.tar.gz

**Step 2:** Unpack the tarball

    tar -xvf node_exporter-1.0.1.linux-amd64.tar.gz
**Step 3:** Move the node exporter binary to /usr/local/bin

    mv node_exporter-*/node_exporter /usr/local/bin
**Step 4:** Create the node_exporter user for the node_exporter service

    useradd -rs /bin/false node_exporter
**Step 5:** Create the node_exporter service

    echo "[Unit]
    Description=Node Exporter
    After=network.target
    
    [Service]
    User=node_exporter
    Group=node_exporter
    Type=simple
    ExecStart=/usr/local/bin/node_exporter
    
    [Install]
    WantedBy=multi-user.target" > /etc/systemd/system/node_exporter.service
**Step 6:** Reload the system daemon and start the node_exporter service

    systemctl daemon-reload && systemctl --now enable node_exporter.service
**Step 7:** Check the status of node_exporter

    systemctl status node_exporter

## Checking the Stats
The stats will now be viable on http://localhost:9182 

## Viewing the Graphs 
There's two options for this, which is installing and self-hosting Grafana & configuring Prometheus collector as a data source, or I can just create a quick dashboard for you on my box. 

If you want me to host this: 
 - Open port 9100 to the remote IP 51.89.199.132
 - Let me know you want your dashboard setting up!


If you want to self-host this: 
 - Check out the guide [here](https://devconnected.com/how-to-setup-grafana-and-prometheus-on-linux/)
