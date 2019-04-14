# Snipe-it Sparta Inventory App
## Description
Snipe-it is a php app built on laravel framework and its open source. This repo creates a local environment for the app using docker and ansible.

## DevOps tools
- Ansible - Configuration Management
- Docker - Docker images, Swarm Cluster and Overlay network
- Vagrant & VirtualBox - Virtual Machines

## How it works ?
- Clone the repo
- Run vagrant up

## Information about the infrastructure
Vargant up brings up three Virtual machines. Ansible is used as the Configuration management tool to provision these machines. Docker pulls the Snipe-it and MySQL 5.6 docker image from the docker hub, creates and runs the containers. Docker uses --link flag to allow communication between two running containers, this is achievable if both the containers were running on the same host. In order to link to a container running on a different host, docker swarm and overlay network was used. Docker swarm is used to create a cluster and then overlay network is used to create a network and attach the containers to it, so that it can be discovered by the docker daemon from external host.

## Terminating
- Run vagrant destroy
- Remember to clear token.yml file as new token will be generated when you run vagrant up again

## Useful Links
- Snipe-it docker documentation: https://snipe-it.readme.io/docs/docker
- Docker Swarm and Overlay network: https://dzone.com/articles/creating-a-docker-overlay-network
