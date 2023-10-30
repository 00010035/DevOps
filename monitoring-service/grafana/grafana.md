# Install Grafana
## 1. Установка Grafana в систему
~~~
sudo apt install libfontconfig
~~~
## 2. Войдите в официальный сайт для того чтобы скачать самый акутальную версию
~~~
https://grafana.com/grafana/download
~~~
## 3. Установка для Linux
~~~
wget https://dl.grafana.com/enterprise/release/grafana-enterprise_10.1.0_amd64.deb
~~~
## 4. Используйте инструкцию документации
~~~
sudo dpkg -i grafana-enterprise_10.1.0_amd64.deb
~~~
## 5. Активируем сервис
~~~
sudo systemctl daemon-reload
~~~
~~~
sudo systemctl enable grafana-server
~~~
~~~
sudo systemctl start grafana-server
~~~
