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

>defaultRule: Host(domain.com)

- Then you should deploy your Traefik "stack", with the following command: 

`$ docker stack deploy -c traefik-deploy.yml traefik`

*The nice thing with this aproach is that traefik is now independant of anything in the OpenRemote stack.*

- The OpenRemote deployment, has a lot of optional environment variables connected to it. But, basically most of them are optional.
In this deployment script it is (in contrast to the default docker-compose.yml at OpenRemote's repository) **expected** that you have a domain name 
pointing to your server. So, you need to change all the "your.domain" fields in the "docker-compose.yml" file (but, not any addresses with http://localhost..). 

After that you are ready to deploy:
`$ docker stack deploy -c docker-compose.yml openremote`

*If you somehow experience trouble, you may try to revert to older images of the containers in the docker-compose.yml file*
