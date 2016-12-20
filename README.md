Dockerized Wetty
================

This is a dockerized version of Wetty krishnasrinivas (https://github.com/krishnasrinivas/wetty), 
with additional ideas from Robert Szymczak (https://github.com/m451/docker-wetty). Both docker images available in these
repositories are node base, with sized up to 1G. This one is based on alpine-node, which gives 
a docker image of around 100G with all npm modules.

This project is linked to the docker hub, so you may always pull the latest build from any docker environment.

```
docker pull svenihoney/wetty
```

Then you can run the application using:

```
docker run -dt -e REMOTE_SSH_SERVER=10.10.10.10 -e REMOTE_SSH_PORT=22 -e REMOTE_SSH_USER=root -p 3000 --name term  svenihoney/wetty
```
The environment parameters 

- REMOTE_SSH_SERVER
- REMOTE_SSH_PORT
- REMOTE_SSH_USER

are optional and will be used to configure wetty. If not set, a connection to 127.0.0.1:22 using root will be performed.
In order to access the web application, you have to get the IP and PORT it is hosted at within your docker environment. 
You may use "docker ps" or "docker inspect" to get the informations. The following command will return the external PORT back the container is mapped back to you.

```
docker port term 3000
```

You may then access the application using http://DockerHostIP:PORT. You may dynamicly change the login-user by utilizing wetty's HTTP GET syntax, e.g.: 

```
http://DockerHostIP:PORT/wetty/ssh/your-ssh-user
```

Reverse Proxy
-------------

I recommend running the image behind a nginx proxy. Please have a look at https://github.com/jwilder/nginx-proxy,
which is used by the included ![docker compose](docker-compose.yml) file.