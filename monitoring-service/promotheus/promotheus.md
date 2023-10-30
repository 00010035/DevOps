# Install Prometheus
## We need to create a new user without home directory and we will setup directory to /bin/false
~~~
sudo useradd --no-create-home --shell /bin/false prometheus
~~~
## Now we need create folders for prometheus
~~~
sudo mkdir /etc/prometheus
~~~
## Create another folder for library 
~~~
sudo mkdir /var/lib/prometheus
~~~
## Now we need add to this folders owner prometheus
~~~
sudo chown prometheus:prometheus /var/lib/prometheus
~~~
## Go to official website to download prometheus
## official site 
~~~
https://prometheus.io/download/
~~~
## command to download prometheus 
~~~
wget https://github.com/prometheus/prometheus/releases/download/v2.46.0/prometheus-2.46.0.linux-amd64.tar.gz
~~~
## Unarhive files
~~~
tar -xvf <file.tar>
~~~
## Now we go to the unarchive folder and move nessesery files to folder
~~~
sudo mv console* /etc/prometheus/
~~~
~~~
sudo mv prometheus.yml /etc/prometheus/
~~~
## And give an permission to owner
~~~
sudo chown -R prometheus:prometheus /etc/prometheus/
~~~
## We need move bineris to folder /user/local/bin/
~~~
sudo mv prometheus /usr/local/bin/
~~~
~~~
sudo mv promtool /usr/local/bin/
~~~
## And give an permisiion 
~~~
sudo chown prometheus:prometheus /usr/local/bin/prom*
~~~
## Create service file for prometheus
~~~
sudo vim /etc/systemd/system/prometheus.service
~~~
## And write commands to this file
~~~
[Unit]
Description=Prometheus
Wants=network-online.target
After=network-online.target

[Service]
User=prometheus
Group=prometheus
Type=simple
ExecStart=/usr/local/bin/prometheus \
    --config.file /etc/prometheus/prometheus.yml \
    --storage.tsdb.path /var/lib/prometheus/ \
    --web.console.templates=/etc/prometheus/consoles \
    --web.console.libraries=/etc/prometheus/console_libraries

[Install]
WantedBy=multi-user.target
~~~
## And now we need to start service that's we created 
~~~
sudo systemctl start prometheus
~~~
## Checking status of prometheus 
~~~
sudo systemctl status prometheus
~~~
## After we check that's all rinning add to aoutostart 
~~~
sudo systemctl enable promrtheus
~~~
