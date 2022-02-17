# openremote-swarm-traefik
## Swarm stack setup with Traefik as proxy service
*HAProxy seems to be a pretty integral part of OpenRemote and the following setup has not been tested extensively. Therefore
you may be running a risk by using this in production and are encouraged to use the default setup provided by the OpenRemote project.*

### Prerequsits
The following setup assumes that you have initialized Swarm by docker (Dockers cluster solution), it is very easy to setup with one or two commands.

### Setup
The setup consists of three files; **traefik.yml**, **traefik-deploy.yml** and **docker-compose.yml**

- Start by creating an overlay network. This network can late be used for other services than OpenRemote ex. a website or what ever..

`$ docker network create --driver=overlay traefik`

- Traefik needs some configuration, we will provide those in a separate file: **traefik.yml** you need to change two lines in that file.
> email: your@email.com
...
defaultRule: Host(`domain.com`)

- 

`$ docker stack deploy -c traefik-deploy.yml traefik`
