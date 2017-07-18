Provision VMs against Virtual Box

This role provisions virtual machines from a virtual box system which allows running
VBoxManage command. To use this role, you will need to make sure that the system where
virtual box vms will be created is ssh enabled and can be accessed either using the
user name and password pair or using the ssh keys. You will also need to make sure
that there is an ubuntu 16.04 image on your current virtual box environment which
can be used to clone new machines. The image should have both python 2.x and docker
already installed. The configuration file is in vars/vb.yml. You should create your
own configuration file by copy and change that file according to your own environment.

To use this role to provision VirtualBxo vms once you create a configuration file like
vars/vb.yml, and named it myvb.yml, you can run the following command in the root directory of the project,
not in the directory where this file is located::

    ansible-playbook -e "mode=apply env=myvb cloud_type=vb password=xxxxx" procluster.yml
    
Replace the xxxxx in the command with your VirtualBox environment password, the user
id should be configured in the auth section in the vars/myvb.yml file.

To remove all these VMs, you can run the following command which will stop all the
vms and completely remove these vms from your VirtualBox environment::

    ansible-playbook -e "mode=destroy env=myvb cloud_type=vb password=xxxxx" procluster.yml
