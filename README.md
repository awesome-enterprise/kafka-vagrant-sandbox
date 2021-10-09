# kafka-vagrant-sandbox

## Content

In case you need a local cluster providing Kafka with ZooKeeper cluster, you are in right place.

* [Apache Kafka 3.0.0](https://kafka.apache.org/30/documentation.html)
* [Apache ZooKeeper 3.7.0](https://zookeeper.apache.org/doc/r3.7.0/index.html)

## Prerequisites
* [Vagrant](https://www.vagrantup.com) (tested with 2.2.18)
* [VirtualBox](http://virtualbox.org) (tested with 6.1.26)
* [Ansible]() (tested with 4.6.0)

# Install instructions on linux
* [Vagrant](https://www.vagrantup.com/downloads)
* [VirtualBox](https://www.virtualbox.org/wiki/Linux_Downloads)
* [Ansible](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html#installing-and-upgrading-ansible-with-pip)
* [Ansible Config](https://github.com/ansible/ansible/blob/stable-2.11/examples/ansible.cfg) should be placed to `/etc/ansible/ansible.cfg`


# Version checking
* Vagrant: 
  `vagrant --version`
* VirtualBox: 
  `vboxmanage --version`
* Ansible: 
`python -c 'from ansible_collections.ansible_release import ansible_version; print(ansible_version)'`


## Init

```bash
git clone https://github.com/awesome-enterprise/kafka-vagrant-sandbox.git
vagrant up
```

## Cluster

The result if everything wents fine should be

![Kafka Zookeeper Cluster](docs/images/kafka-zookeeper-cluster-diagram.png)
