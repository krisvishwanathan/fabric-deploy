# Hyperledger Fabric Deployment

This ansible playbook project will accomplish the following tasks

 - Provision virtual machine nodes to participate in fabric network
 - Install necessary hyperledger dependent libraries and packages
 - Setup overlay network so containers can communicate cross multiple docker host
 - Setup kubernetes 1.7.0 (if choose to do that)
 - Install registrator and dns services so that containers can be referenced by name
 - Build hyperledger fabric artifacts
 - Run hyperledger fabric tests
 - Generate fabric network certificats, genesis blocks, transaction file etc
 - Push new or tagged fabric images onto all docker hosts
 - Deploy fabric network
 
## Status

In development

## Requirements

- [Install Ansible](http://docs.ansible.com/ansible/intro_installation.html)
- [Ubuntu 16.04 machines] (https://cloud-images.ubuntu.com/releases/16.04/)
- Clone this project into a directory.

If you will be using an Ubuntu system as Ansible controller, then you can
easily setup an environment by running the following script. If you have
other system as your Ansible controller, you can do similar steps to setup
the environment, the command may not be exact the same but the steps you
need to do should be identical.

    sudo apt-get update
    sudo apt-get install python-dev python-pip libssl-dev libffi-dev -y
    sudo pip install --upgrade pip
    sudo pip install six==1.10.0
    sudo pip install ansible==2.3.0.0
    git clone https://github.com/litong01/fabric-deploy.git

This project requires that you use Ansible version 2.3.0.0 or above

## Deploy hyperledger fabric onto different environment

### On VirtualBox::

    make changes to vars/vb.yml according to your VirtualBox environment
    export password="your password to vb env"
    
    To deploy:    
    ansible-playbook -e "mode=apply" vb.yml

    To destroy:    
    ansible-playbook -e "mode=destroy" vb.yml

### On OpenStack cloud::

    make changes to vars/os.yml according to your OpenStack cloud
    export password="your password to OpenStack cloud"
    
    To deploy:
    ansible-playbook -e "mode=apply" os.yml

    To destroy:
    ansible-playbook -e "mode=destroy" os.yml


### On AWS cloud::

    make changes to vars/aws.yml according to your aws cloud
    export AWS_SECRET_KEY="your password to aws cloud"
    
    To deploy:
    ansible-playbook -e "mode=apply" aws.yml

    To destroy:
    ansible-playbook -e "mode=apply" aws.yml
