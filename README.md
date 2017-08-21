# Hyperledger Fabric Deployment

Hyperledger fabric-deploy is an ansible project which deploys hybperledger fabric
onto multiple physical or virtual servers.

 - Provision virtual servers to participate in fabric network
 - Install necessary hyperledger dependent libraries and packages
 - Setup kubernetes 1.7.0 or overlay network so that containers can communicate cross multiple docker hosts
 - Install registrator and dns services so that containers can be referenced by name
 - Build hyperledger fabric artifacts (optional)
 - Run hyperledger fabric tests (optional)
 - Generate fabric network certificats, genesis block, transaction blocks
 - Push new or tagged fabric images onto all docker hosts
 - Deploy fabric network
 - Join peers to channels, instantiate chaincode
 
## Status

In development

## Requirements for ansible controller

- [Install Ansible](http://docs.ansible.com/ansible/intro_installation.html)
- [Ubuntu 16.04 machines] (https://cloud-images.ubuntu.com/releases/16.04/)
- Install cloud platform dependent packages such as OpenStack shade or AWS boto 
- Ansible 2.3.0.0 or above

Here is an example on how to make a clean ubuntu system as your ansible controller
If you have other system as your Ansible controller, you can do similar steps to setup
the environment, the command may not be exact the same but the steps you
need to do should be identical.

    sudo apt-get update
    sudo apt-get install python-dev python-pip libssl-dev libffi-dev -y
    sudo pip install --upgrade pip
    sudo pip install six==1.10.0
    sudo pip install ansible==2.3.0.0
    git clone https://github.com/litong01/fabric-deploy.git

## Deploy hyperledger fabric onto different environment

### On VirtualBox::

    1. make changes to vars/vb.yml according to your VirtualBox environment
    2. export password="your password to vb env"
    3. To stand up the fabric network::
        ansible-playbook -e "mode=apply" vb.yml
    4. To tear down the fabric network::
        ansible-playbook -e "mode=destroy" vb.yml

### On OpenStack cloud::

    1. make changes to vars/os.yml according to your OpenStack cloud
    2. export password="your password of your OpenStack cloud account"
    3. To stand up the fabric network::
        ansible-playbook -e "mode=apply" os.yml
    4. To tear down the fabric network::
        ansible-playbook -e "mode=destroy" os.yml

### On AWS cloud::

    1. make changes to vars/aws.yml according to your aws cloud
    2. export AWS_SECRET_KEY="your secret key of your aws account"
    3. To stand up the fabric network::
        ansible-playbook -e "mode=apply" aws.yml
    4. To tear down the fabric network::
        ansible-playbook -e "mode=destroy" aws.yml
