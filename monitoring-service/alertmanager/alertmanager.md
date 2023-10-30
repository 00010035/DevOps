# Установка Alertmanager
## 1. Создание нового юзера
~~~
sudo useradd --no-create-home --shell /bin/false alertmanager
~~~
## 2. Создать каталог для конфигурации файла
~~~
sudo mkdir /etc/alertmanager
~~~
## 3. Загрузите Alertmanager с официального сайта
~~~
wget https://github.com/prometheus/alertmanager/releases/download/v0.26.0/alertmanager-0.26.0.linux-amd64.tar.gz
~~~
## 4. Разархивировать файл, который мы скачали
~~~
tar -xvf <file.tar>
~~~
## 5. Чтобы увидеть, что было загружено, используйте команду «ls»
## 6. Переместите двоичные файлы в «/usr/local/bin»
~~~
sudo mv alertmanager /usr/local/bin/ 
~~~
~~~
sudo mv amtool /usr/local/bin/
~~~
## 7. Добавить разрешение пользователю для папки
~~~
sudo chown alertmanager:alertmanager /usr/local/bin/alertmanager
~~~
## 8. Убедитесь, что у нас есть права на amtools
~~~
sudo chown alertmanager:alertmanager /usr/local/bin/amtool
~~~
## 9. И, наконец, нам нужно переместить последний файл
~~~
sudo mv alertmanager.yml /etc/alertmanager
~~~
## 10. Give an permission for the folder
~~~
sudo chown -R alertmanager:alertmanager /etc/alertmanager/
~~~
## 11. Теперь нам нужно создать сервис alerrtmanager
~~~
sudo vim /etc/systemd/system/alertmanager.service
~~~
## 12. И добавляем конфиг для сервиса
~~~
[Unit]
Description=Alertmanager
Wants=network-online.target
After=network-online.target

[Service]
User=alertmanager
Group=alertmanager
Type=simple
WorkingDirectory=/etc/alertmanager/
ExecStart=/usr/local/bin/alertmanager \
    --config.file=/etc/alertmanager/alertmanager.yml

[Install]
WantedBy=multi-user.target
~~~
## 13. Чтобы запустить alertmanager, нам нужно убедиться, что Prometheus не запущен
~~~
sudo systemctl stop prometheus
~~~
## Необходимо обновить файл prometheus.yml.
~~~
sudo vim /etc/prometheus/prometheus.yml
~~~
## In the config file find Alertmanager config and replace "- alermanager:9093" with "localhost:9093"
## Now we need to reload daemon
~~~
sudo systemctl daemon-reload
~~~
## And now let's start Prometheus and Alertmanager
~~~
sudo systemctl start prometheus
~~~
~~~
sudo systemctl start alertmanager
~~~
## And check that's all is running 
~~~
sudo systemctl status prometheus
~~~
~~~
sudo systemctl status alertmanager
~~~
