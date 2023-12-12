# Docker Swarm Setup

## Introduction

This repository provides instructions for setting up a Docker Swarm with a manager and two worker nodes on CentOS 7 servers.

## Server Configuration

### Swarm Manager
1. Run the following command on all three servers to update the system:
    ```bash
    sudo yum update -y
    ```

2. On the CentOS 7 Swarm Manager:
    ```bash
    # Remove existing Docker installations
    sudo yum remove -y docker \
                      docker-client \
                      docker-client-latest \
                      docker-common \
                      docker-latest \
                      docker-latest-logrotate \
                      docker-logrotate \
                      docker-engine

    # Install Docker dependencies and repository
    sudo yum install -y yum-utils
    sudo yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo

    # Install Docker and related tools
    sudo yum install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

    # Start Docker service
    sudo systemctl start docker

    # Create Docker group and add user to the group
    sudo groupadd docker
    sudo usermod -aG docker $USER
    newgrp docker

    # Enable Docker services to start on boot
    sudo systemctl enable docker.service
    sudo systemctl enable containerd.service

    # Verify Docker installation
    docker run hello-world

    # Install additional dependencies
    sudo yum install -y device-mapper-persistent-data lvm2

    # Initialize Docker Swarm
    docker swarm init --advertise-addr [Private IP of the Swarm Manager]

    # Copy the `docker swarm join` command provided (to be used on the workers after they have Docker set up).
    ```

### Swarm Workers
3. On the CentOS 7 Swarm Workers:
    ```bash
    # Remove existing Docker installations
    sudo yum remove -y docker \
                      docker-client \
                      docker-client-latest \
                      docker-common \
                      docker-latest \
                      docker-latest-logrotate \
                      docker-logrotate \
                      docker-engine

    # Install Docker dependencies and repository
    sudo yum install -y yum-utils
    sudo yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo

    # Install Docker and related tools
    sudo yum install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

    # Start Docker service
    sudo systemctl start docker

    # Create Docker group and add user to the group
    sudo groupadd docker
    sudo usermod -aG docker $USER
    newgrp docker

    # Enable Docker services to start on boot
    sudo systemctl enable docker.service
    sudo systemctl enable containerd.service

    # Verify Docker installation
    docker run hello-world

    # Install additional dependencies
    sudo yum install -y device-mapper-persistent-data lvm2

    # Run the earlier copied `docker swarm join` command received from the Swarm Manager.
    # Example only:
    docker swarm join --token SWMTKN-1-058yz85mc76fsf1ldm7w2evqjuit5nsdksrzqbtgtnaetnze1m-4w76mpkecb5y1utjexhdhlly8 172.31.37.43:2377
    ```

4. Back on the Swarm Manager:
    ```bash
    # Verify Swarm nodes
    docker node ls
    ```

This completes the Docker Swarm setup with a manager and two worker nodes. Make sure to replace placeholders like `[Private IP of the Swarm Manager]` with the actual private IP address of your Swarm Manager. Also, include any additional details specific to your setup or project.
