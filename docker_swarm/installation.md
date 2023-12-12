# Docker Swarm Setup

## Introduction

This repository provides instructions for setting up a Docker Swarm with a manager and two worker nodes. Follow the steps below to configure the Swarm on CentOS 7 servers.

## Server Configuration

### Swarm Manager
1. Run the following command on all three servers to update the system:
    ```bash
    sudo yum update -y
    ```

2. On the CentOS 7 Swarm Manager:
    ```bash
    sudo yum remove -y docker \
                      docker-client \
                      docker-client-latest \
                      docker-common \
                      docker-latest \
                      docker-latest-logrotate \
                      docker-logrotate \
                      docker-engine

    sudo yum install -y yum-utils
    sudo yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo

    sudo yum install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

    sudo systemctl start docker

    sudo groupadd docker

    sudo usermod -aG docker $USER

    newgrp docker

    sudo systemctl enable docker.service
    sudo systemctl enable containerd.service

    docker run hello-world

    sudo yum install -y device-mapper-persistent-data lvm2

    docker swarm init \
    --advertise-addr [Private IP of the Swarm Manager]

    # Copy the `docker swarm join` command provided (to be used on the workers after they have Docker setup).
    ```

### Swarm Workers
3. On the CentOS 7 Swarm Workers:
    ```bash
    sudo yum remove -y docker \
                      docker-client \
                      docker-client-latest \
                      docker-common \
                      docker-latest \
                      docker-latest-logrotate \
                      docker-logrotate \
                      docker-engine

    sudo yum install -y yum-utils
    sudo yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo

    sudo yum install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

    sudo systemctl start docker

    sudo groupadd docker

    sudo usermod -aG docker $USER

    newgrp docker

    sudo systemctl enable docker.service
    sudo systemctl enable containerd.service

    docker run hello-world

    sudo yum install -y device-mapper-persistent-data lvm2

    # Run the earlier copied `docker swarm join` command received from the Swarm Manager.
    # Example only:
    docker swarm join --token SWMTKN-1-058yz85mc76fsf1ldm7w2evqjuit5nsdksrzqbtgtnaetnze1m-4w76mpkecb5y1utjexhdhlly8 172.31.37.43:2377
    ```

4. Back on the Swarm Manager:
    ```bash
    docker node ls
    ```

This completes the Docker Swarm setup with a manager and two worker nodes.

For additional information or troubleshooting, refer to the Docker documentation.
