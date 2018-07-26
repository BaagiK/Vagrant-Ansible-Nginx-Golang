## Vagrant-Ansible-Nginx-Golang

- Launching 3 RHEL7 VMs using Vagrant and Virtual Box.
- Integrating Ansible with vagrant to execute playbook.yml
- Using Ansible:
  1. configuring 1 VM - "web" as NGINX web server with round-robin load balancing
  2. configuring 2 VMs - "app-node1 & app-node2" to host sample Golang application as part og NGINX loadbalancing configuraiton

- Save all files in to a folder used as vagrant workspace.
- From that folder, run:

`vagrant init` for the first time, and 

`vagrant init --provision` for subsequent times

web - 192.168.2.101

app-node1 - 192.168.2.102

app-node2 - 192.168.2.103
