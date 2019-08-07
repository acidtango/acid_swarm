# Acid Swarm

Acid Swarm is a docker stack to get your Docker Swarm cluster ready in minutes.

## Requisites

This compose file was created to be deployed inside a Docker Swarm Cluster. For more info on how to
create one check the [Docker Documentation](https://docs.docker.com/engine/swarm/swarm-tutorial/).

You could also use our [Terraform template](https://github.com/acidtango/terracid_tango/tree/with_docker)
to deploy a Docker Swarm cluster to AWS.

## What's inside

### Swarmpit

To monitorize the Docker Swarm cluster we use [Swarmpit](https://swarmpit.io/), it allows us to see in which nodes the applications are deployed, check the logs for each application and the resources used by each node. It also give us some more functionality, like deploy stacks, add an image registry and manage docker secrets.

Once the stack is deployed, you can access it in `swarmpit.yourdomain.com`.

### Traefik

To redirect the traffic to the correct container we use [Traefik](https://traefik.io/). With Traefik you can configure a set of rules to determine what petition goes to what container. This is configured directly in the docker-compose files and it continously updates it's configuration so restarts are not needed.

Once the stack is deployed, you can check those rules in `traefik.yourdomain.com`.

### Cluster cleanup

We also add a container with a restart policy of `24h` which cleans up unused images and containers every 24 hours.

## How to use it

All the following commands must be executed in a `manager node`.

First, we will create the [overlay network](https://docs.docker.com/network/overlay/) that Traefik
will use to distribute the load across the entire cluster. We are naming this network `traefik-net`,
but feel free to give it the name you want. Just remember to change the name in the docker-compose file too.

```sh
docker network create -d overlay traefik-net
```

Then clone this repository

```sh
git clone https://github.com/acidtango/acid_swarm.git
```

and deploy the stack specifying the domain to use for Traefik rules.

```sh
DOMAIN_NAME={your-domain} docker stack deploy -c swarm_init/docker-compose.yml infrastructure
```

## Contributing

Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.

## License

[MIT](LICENSE.md)
