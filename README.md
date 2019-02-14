# swarm_init
Docker Stack to initialize a Swarm Cluster with [Traefik](https://docs.traefik.io/) as reverse proxy
and [Swarmpit](https://swarmpit.io/) to visualize the cluster.

# Requisites

This compose file was created to be deployed inside a Swarm Cluster. For more info on how to
create a Swarm cluster check the [Docker Docs](https://docs.docker.com/engine/swarm/swarm-tutorial/).

You could also use our [terraform template](https://github.com/acidtango/terracid_tango/tree/with_docker)
to deploy a Swarm cluster in AWS.

# Usage

All the following commands must be executed in a Swarm Manager node.

First, we will create the [overlay network](https://docs.docker.com/network/overlay/) that Traefik
will use to distribute the load across the entire Cluster. We are naming this network `traefik-net`,
but feel free to give it the name you want. Just remember to change the name in the compose file too.

```
docker network create -d overlay traefik-net
```

Clone this repository and deploy the stack specifying the domain to use for Traefik rules.

```
$ git clone https://github.com/acidtango/swarm_init.git
$ DOMAIN_NAME=your-domain.com docker stack deploy -c swarm_init/docker-compose.yml infrastructure
```
