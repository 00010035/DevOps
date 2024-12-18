# Zabbix Agent 2 Installation Guide

## Introduction
This guide details the installation and configuration of **Zabbix Agent 2** for systems requiring Docker integration or advanced plugin support. For other package requirements, use the standard Zabbix Agent.

### Key Differences Between Zabbix Agent and Agent 2
- **Zabbix Agent:** Lightweight, suitable for traditional monitoring setups.
- **Zabbix Agent 2:** Built with Go, supports additional plugins, ideal for modern workloads like **Docker**.

## Installing Zabbix Agent 2

### Step 1: Choose Your Platform
Go to the [official Zabbix website](https://www.zabbix.com/download?os_distribution=ubuntu) and select the following options:

- **Zabbix version:** 7.2
- **OS Distribution:** Ubuntu
- **OS Version:** 24.04
- **Zabbix Component:** Agent 2

### Step 2: Install Zabbix Repository
Run the following commands to add the Zabbix repository:
```bash
sudo -s
wget https://repo.zabbix.com/zabbix/7.2/release/ubuntu/pool/main/z/zabbix-release/zabbix-release_latest_7.2+ubuntu24.04_all.deb
dpkg -i zabbix-release_latest_7.2+ubuntu24.04_all.deb
apt update
```

### Step 3: Install Zabbix Agent 2
Run the following command to install Zabbix Agent 2 and its plugins:
```bash
apt install zabbix-agent2 zabbix-agent2-plugin-*
```

### Step 4: Start Zabbix Agent 2 Process
Start the Zabbix Agent 2 process and enable it to start at system boot:
```bash
systemctl restart zabbix-agent2
systemctl enable zabbix-agent2
```

## Next Steps
Your Zabbix Agent 2 setup is now complete. If you need further customization or integration, refer to the [Zabbix documentation](https://www.zabbix.com/documentation/current).
