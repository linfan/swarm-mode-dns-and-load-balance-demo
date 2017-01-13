whoami
======

Simple HTTP docker service that prints it's container ID

## Build it

    $ docker build -t flin/whoami .

## Run it

    $ docker run -dt -p 8000:8000 --name whoami flin/whoami
    
    $ curl $(hostname -i):8000
    I'm d819ec8ff4cd

## Run it in swarm mode

    $ docker service create --name whoami --replicas 3 --publish 8000:8000 flin/whoami
    
    $ curl $(hostname -i):8000
    I'm d819ec8ff4cd
    $ curl $(hostname -i):8000
    I'm c2bf30b3fb17
    $ curl $(hostname -i):8000
    I'm a2ccf532b47d
