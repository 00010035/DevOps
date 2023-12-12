# Docker Swarm Node Management

## Introduction

This guide covers the management of nodes within a Docker Swarm. Learn how to list nodes, inspect node details, promote and demote nodes, remove nodes, and manage swarm-wide operations.

## Docker Node Commands

- **demote:** Demotes one or more nodes from manager in the swarm
- **inspect:** Displays detailed information on one or more nodes
- **ls:** Lists nodes in the swarm
- **promote:** Promotes one or more nodes to manager in the swarm
- **ps:** Lists tasks running on one or more nodes, defaults to current node
- **rm:** Removes one or more nodes from the swarm
- **update:** Updates a node

## Docker Swarm Commands

- **ca:** Displays and rotates the root CA
- **init:** Initializes a swarm
- **join:** Joins a swarm as a node and/or manager
- **join-token:** Manages join tokens
- **leave:** Leaves the swarm
- **unlock:** Unlocks swarm
- **unlock-key:** Manages the unlock key
- **update:** Updates the swarm

## Managing Swarm Nodes

### Listing Nodes:

```bash
docker node ls

### Inspecting a Node:

```bash
docker node inspect [NODE_NAME]
```

### Promoting a Worker to a Manager:

```bash
docker node promote [NODE_NAME]
```

### Demoting a Manager to a Worker:

```bash
docker node demote [NODE_NAME]
```

### Removing a Node from the Swarm (node must be demoted first):

```bash
docker node rm -f [NODE_NAME]
```

### Make a Node Leave the Swarm:

```bash
docker swarm leave
```

### Getting the Join-Token:

```bash
docker swarm join-token [worker|manager]
```

### Make the Node Rejoin the Swarm:

```bash
docker swarm join --token [TOKEN] <PRIVATE_IP>:2377
```

## Conclusion

This guide provides essential commands for managing Docker Swarm nodes. Customize the commands based on your swarm configuration and requirements.
```
