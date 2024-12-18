# Zabbix Client Installation Guide

## Installing Zabbix on the Master Server (Client)

### Step 1: Download Zabbix Packages
Go to the [official Zabbix website](https://www.zabbix.com/download?os_distribution=ubuntu) and select the following options:

- **Zabbix version:** Latest (7.2)
- **OS Distribution:** Ubuntu
- **OS Version:** 24.04
- **Zabbix Component:** Server, Frontend, Agent
- **Database:** PostgreSQL
- **Web Server:** Nginx

### Step 2: Add Zabbix Repository
Run the following commands to add the Zabbix repository:
```bash
sudo -s
wget https://repo.zabbix.com/zabbix/7.2/release/ubuntu/pool/main/z/zabbix-release/zabbix-release_latest_7.2+ubuntu24.04_all.deb
dpkg -i zabbix-release_latest_7.2+ubuntu24.04_all.deb
apt update
```

### Step 3: Install Zabbix Server, Frontend, and Agent
Run the following command to install Zabbix components:
```bash
apt install zabbix-server-pgsql zabbix-frontend-php php8.3-pgsql zabbix-nginx-conf zabbix-sql-scripts zabbix-agent
```

### Step 4: Create Initial Database
Ensure the database server is running, then execute the following commands on your database host:
```bash
sudo -u postgres createuser --pwprompt zabbix
sudo -u postgres createdb -O zabbix zabbix
```

On the Zabbix server host, import the initial schema and data:
```bash
zcat /usr/share/zabbix/sql-scripts/postgresql/server.sql.gz | sudo -u zabbix psql zabbix
```

### Step 5: Configure the Database for Zabbix Server
Edit the Zabbix server configuration file:
```bash
nano /etc/zabbix/zabbix_server.conf
```
Set the database password by adding the following line:
```conf
DBPassword=<your_database_password>
```

### Step 6: Configure PHP for Zabbix Frontend
Edit the Zabbix Nginx configuration file:
```bash
nano /etc/zabbix/zabbix_nginx.conf
```
Set the listening port and server name:
```nginx
listen 8080;
server_name example.com; # Replace with your domain name
```

### Step 7: Start Zabbix Server and Agent Processes
Start Zabbix server and agent processes, and enable them to start at system boot:
```bash
systemctl restart zabbix-server zabbix-agent nginx php8.3-fpm
systemctl enable zabbix-server zabbix-agent nginx php8.3-fpm
```

Your Zabbix server and client setup is now complete!
