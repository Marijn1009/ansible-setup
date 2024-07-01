# ansible-setup
Learning project: Setting up a jump host and Ansible to manage multiple servers.

Techniques used:
* Ansible
* Docker
* Linux

## Setup jump host
**Why a jump host?**  
It is a central boundary between networks. Here it will be the boundary between the open internet, and a private network of containers. By setting up one jump host, all security, access and logging can be controlled on the jump host. 

1. Create a Docker network
    * The default is a bridged network, where containers can talk to each other. 
    * The goal is to be able to ssh from host pc onto the central jump host container, and from there access the other containers.  

```
docker network create network-ansible-setup
```

2. Run Docker containers
    * Detached: Run in background and give control back to terminal.
    * Rockylinux: RHEL-compatible and based on CentOS. But unlike the older CentOS 8 / 9 versions, this one still gets updates. 

```
docker run -d --name jump_host --network network-ansible-setup rockylinux/rockylinux
docker run -d --name server1 --network network-ansible-setup rockylinux/rockylinux
docker run -d --name server2 --network network-ansible-setup rockylinux/rockylinux
```