# Keycloak cluster Ansible

Sets up Keycloak cluster (version>=17.0.0) using Ansible. There are three roles which include database cluster (MariaDB by default), Keycloak app (with Infinispan) and balancer (HAProxy). Default scheme is 4 nodes (3+1).

Also you can use any role separately (to install MariaDB with Galera cluster, for example)

## Platforms

- Ubuntu 20.04
- CentOS 7
- Debian 10
- RHEL 7

It could work on CentOS 8 or Ubuntu 18, etc, have not checked
## Requirements

- Ansible >=2.9.6 on your deploy machine `sudo yum install ansible`(CentOS or RHEL) and `sudo apt install ansible`(Ubuntu or Debian)


Don't forget to put your keys on target hosts and set or turn off firewalld and SELinux (CentOS 7)

## Install

Put your IP addresses into 'hosts' file and run
```sh
ansible-playbook -i hosts start.yml
```

Inventory example:

```sh
[nodes]
node1 ansible_host=<node1-ip-address>
node2 ansible_host=<node2-ip-address>
node3 ansible_host=<node3-ip-address>

[balance]
balancer ansible_host=<balancer-ip-address>

[all:vars]
keycloak_port=8080 (or another wanted port)
```


You can change Keycloak version, access port and admin password in roles/keycloak/default/main.yml.

Default Keycloak version is 17.0.1, access port - 8080

## Result

Keycloak cluster is availible on:

http://IP-balancer-node:80

https:/IP-balancer-node:443

Certain node:

http://IP-node:your_port


If you have true certificate, you can put it on proxy host.
