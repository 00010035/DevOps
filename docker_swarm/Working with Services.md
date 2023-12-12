# Docker Service Management

## Introduction

This guide covers essential Docker service commands for creating, inspecting, logging, listing, scaling, and updating services.

## Docker Service Commands

- **create:** Creates a new service
- **inspect:** Displays detailed information on one or more services
- **logs:** Fetches the logs of a service or task
- **ls:** Lists services
- **ps:** Lists the tasks of one or more services
- **rm:** Removes one or more services
- **rollback:** Reverts changes to a service's configuration
- **scale:** Scales one or multiple replicated services
- **update:** Updates a service

## Service Management

### Creating a Service:

```bash
docker service create -d --name [NAME] \
-p [HOST_PORT]:[CONTAINER_PORT] \
--replicas [REPLICAS] \
[IMAGE] [CMD]

### List Services:

```bash
docker service ls
```

### Inspecting a Service:

```bash
docker service inspect [NAME]
```

### Get Logs for a Service:

```bash
docker service logs [NAME]
```

### List Tasks of a Service:

```bash
docker service ps [NAME]
```

### Scale a Service Up or Down:

```bash
docker service scale [NAME]=[REPLICAS]
```

### Update a Service:

```bash
docker service update [OPTIONS] [NAME]
```

## Example Usage

### Creating Nginx Service:

```bash
docker service create -d --name nginx_service -p 8080:80 --replicas 2 nginx:latest
```

### List Swarm Services:

```bash
docker service ls
```

### Inspect Nginx Service:

```bash
docker service inspect nginx_service
```

### View Running Tasks for Nginx Service:

```bash
docker service ps nginx_service
```

### Scale Nginx Service to 3 Replicas:

```bash
docker service scale nginx_service=3
```
