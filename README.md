whoami and curl
======

Demo for swarm mode servcie dns and load balance.

## Docker images

- `whoami`: Simple HTTP docker service that prints it's container ID
- `curl`: Simple HTTP client image base on alpine

## Build it

    $ docker build -t flin/whoami whoami
    $ docker build -t flin/curl curl 

## Run it in swarm mode

    $ docker network create demo --driver overlay
    $ docker service create --name whoami --network demo --replicas 3 --publish 8000:8000 flin/whoami
    $ docker service create --name curl --network demo flin/curl

SSH into the node which curl container located, find its id as <curl-container-id>.

Try to access whoami service via its name.

    $ docker exec <curl-container-id> curl -s whoami:8000
    I'm d819ec8ff4cd
    $ docker exec <curl-container-id> curl -s whoami:8000
    I'm c2bf30b3fb17
    $ docker exec <curl-container-id> curl -s whoami:8000
    I'm a2ccf532b47d
