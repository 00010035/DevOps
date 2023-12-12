# Docker Overlay Networks in Swarm

## Create a Basic Overlay Network:

```bash
docker network create -d overlay [NAME]
```

### Create a Service with an Overlay Network:

```bash
docker service create -d --name [NAME] \
--network [NETWORK] \
-p [HOST_PORT]:[CONTAINER_PORT] \
--replicas [REPLICAS] \
[IMAGE] [CMD]
```

### Add a Service to a Network:

```bash
docker service update --network-add [NETWORK] [SERVICE]
```

### Remove a Service from a Network:

```bash
docker service update --network-rm [NETWORK] [SERVICE]
```

## Examples

### Create a Basic Overlay Network:

```bash
docker network create -d overlay my_overlay
```

### Create an Encrypted Overlay Network:

```bash
docker network create -d overlay --opt encrypted encrypted_overlay
```

### Inspect Encrypted Overlay Network:

```bash
docker network inspect encrypted_overlay
```

### Inspect Basic Overlay Network:

```bash
docker network inspect my_overlay
```

### Create a Service using the Basic Overlay Network:

```bash
docker service create -d --name nginx_overlay --network my_overlay -p 8081:80 --replicas 2 nginx:latest
```

### Add Basic Overlay Network to an Existing Service:

```bash
docker service update --network-add my_overlay nginx_service
```

### Inspect Nginx Service:

```bash
docker service inspect nginx_service
```

### Remove Basic Overlay Network from Nginx Service:

```bash
docker service update --network-rm my_overlay nginx_service
```

### Inspect Nginx Service After Removal:

```bash
docker service inspect nginx_service
```

### Remove Encrypted Overlay Network:

```bash
docker network rm encrypted_overlay
```

## Explanation

- **Overlay Networks:** Overlay networks allow containers within a Swarm to communicate seamlessly, regardless of the nodes they are running on. This facilitates the creation of highly scalable and distributed applications.

- **Creating Overlay Networks:** The `docker network create` command is used to create overlay networks, specifying the driver as `overlay`.

- **Service Networking:** When creating services, the `--network` option is used to associate them with specific overlay networks, enabling communication between services.

- **Adding/Removing Networks:** The `docker service update` command is used to add or remove services from overlay networks, providing flexibility in network configurations.

- **Encrypted Overlay Networks:** The `--opt encrypted` option can be added during network creation to enable encryption for enhanced security.
