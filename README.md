Bitcoind for Docker
===================

[![Docker Stars](https://img.shields.io/docker/stars/bartoszmilczarek/bitcoind.svg)](https://hub.docker.com/r/bartoszmilczarek/bitcoind/)
[![Docker Pulls](https://img.shields.io/docker/pulls/bartoszmilczarek/bitcoind.svg)](https://hub.docker.com/r/bartoszmilczarek/bitcoind/)
[![ImageLayers](https://images.microbadger.com/badges/image/bartoszmilczarek/bitcoind.svg)](https://microbadger.com/#/images/bartoszmilczarek/bitcoind)
[![Image version](https://images.microbadger.com/badges/version/bartoszmilczarek/bitcoind.svg)](https://microbadger.com/images/bartoszmilczarek/bitcoind)

Docker image that runs the Bitcoin bitcoind node in a container for easy deployment.


Requirements
------------

* Physical machine, cloud instance, or VPS that supports Docker (i.e. [Vultr](http://bit.ly/1HngXg0), [Digital Ocean](http://bit.ly/18AykdD), KVM or XEN based VMs) running Ubuntu 14.04 or later (*not OpenVZ containers!*)
* At least 100 GB to store the block chain files (and always growing!)
* At least 1 GB RAM + 2 GB swap file

Recommended and tested on unadvertised (only shown within control panel) [Vultr SATA Storage 1024 MB RAM/250 GB disk instance @ $10/mo](http://bit.ly/vultrbitcoind).  Vultr also *accepts Bitcoin payments*!

Quick Start
-----------

1. Create a `bitcoind-data` volume to persist the bitcoind blockchain data, should exit immediately.  The `bitcoind-data` container will store the blockchain when the node container is recreated (software upgrade, reboot, etc):

        docker volume create --name=bitcoind-data
        docker run -v bitcoind-data:/bitcoin --name=bitcoind-node -d \
            -p 8333:8333 \
            -p 127.0.0.1:8332:8332 \
            bartoszmilczarek/bitcoind

2. Verify that the container is running and bitcoind node is downloading the blockchain

        $ docker ps
        CONTAINER ID        IMAGE                         COMMAND             CREATED             STATUS              PORTS                                              NAMES
        696486017c8d        bartoszmilczarek/bitcoind     "btc_oneshot"       2 seconds ago       Up 1 seconds        127.0.0.1:8332->8332/tcp, 0.0.0.0:8333->8333/tcp   bitcoind-node

3. You can then access the daemon's output thanks to the [docker logs command]( https://docs.docker.com/reference/commandline/cli/#logs)

        docker logs -f bitcoind-node

4. Run bitcoin node from docker compose:
        
        docker-compose -f docker-compose-bitcoind.yml up


Documentation
-------------

* Additional documentation in the [docs folder](docs).
