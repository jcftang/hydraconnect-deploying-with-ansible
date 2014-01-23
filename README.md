Demo of Deploying with Ansible 

This repository contains a small example project on how to deploy haproxy
and apache. There are three virtual machines in this example.

Before you start you will need to install

* Vagrant 1.4.x
* Virtualbox 4.3.x
* Ansible 1.4.x

To experiment with this example:

   $ vagrant up
   $ source ./hacking/env-setup
   $ ansible-playbook -i hosts.vagrant site.yml

Then try hitting the example loadbalancer and try turning off one of the backend webservers

   $ ab -t 60 -c 10 -n 1000 http://192.168.250.100/

The stats can be viewed at http://192.168.250.100:8080
