
# Portainer Server Installation Guide

Follow these steps to install and set up Portainer Server on your system.

## Step 1: Create Volume for Portainer Data

First, create the volume that Portainer Server will use to store its database:

```sh
docker volume create portainer_data
```

## Step 2: Download and Install Portainer Server Container

Next, download and install the Portainer Server container by running the following command:

```sh
docker run -d -p 8000:8000 -p 9443:9443 --name portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ce:latest
```

## Step 3: Logging In

Once the installation is complete, you can log into your Portainer Server instance by opening a web browser and navigating to:

[https://localhost:9443](https://localhost:9443)

Enjoy managing your Docker environment with Portainer!

