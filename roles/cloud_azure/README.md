Provision VMs in Azure cloud using ansible
http://docs.ansible.com/ansible/latest/guide_azure.html

Install Azure CLI 2.0
https://docs.microsoft.com/en-us/cli/azure/install-azure-cli

azure - create or terminate a virtual machine in azure
azure_rm_deployment - Create or destroy Azure Resource Manager template deployments

https://github.com/Azure/azure-quickstart-templates/blob/master/ansible-advancedlinux/azuredeploy.json
Install Azure Python SDK. At the time of this writing, the latest supported version is 2.0.0rc5. With this version, the package msrestazure needs to be installed independently. Additionally, we will install the package DNS Python so that we can do DNS checks in Ansible playbooks (to make sure that DNS names are not taken)

https://docs.microsoft.com/en-us/azure/virtual-machines/linux/ansible-create-vm


very good azure ansible playbook -
https://github.com/Blaag/azure/edit/master/create-iperf-vm.yml

https://docs.ansible.com/ansible/guide_azure.html

https://github.com/erjosito/ansible-azure-lab

http://docs.ansible.com/ansible/latest/azure_rm_deployment_module.html

Azure Access INFO
======
SubscriptionId: 2bf26bcf-d4d5-4ef2-9642-0caa4baf96d6
tenentid: 543667c3-62c7-42f4-9a24-972a3285b46e
client id: 9b7bb3f1-84d8-42cc-9dda-e2e01a1f2a89
secret: VXOcvWi0xmHeyR381w+p5Ktm9V8k5p5A7y+uOBZ/81Y=

subscription_id=2bf26bcf-d4d5-4ef2-9642-0caa4baf96d6
client_id=9b7bb3f1-84d8-42cc-9dda-e2e01a1f2a89
secret=VXOcvWi0xmHeyR381w+p5Ktm9V8k5p5A7y+uOBZ/81Y=
tenant=543667c3-62c7-42f4-9a24-972a3285b46e


Pre-reqs 
---------

To use ansible to work with AWS, python library like boto and boto3 must be installed:
-----
sudo pip install azure==2.0.0rc5


Nice to have:
-------------
sudo pip install msrestazure dnspython packaging

Azure Blockchain template -
https://azure.microsoft.com/en-us/resources/templates/blockchain/

-- TODO - 
---------------------------
- { name: http, protocol: Tcp, source_address_prefix: "0.0.0.0/0", destination_port_range: 80, access: Allow, priority: 104,direction: Inbound }
- { name: ICMP_IPv4_IN, protocol: *, source_address_prefix: "0.0.0.0/0", destination_port_range: -1, access: Allow, priority: 105,direction: Inbound }
- { name: ICMP_IPv4_OUT, protocol: *, source_address_prefix: "0.0.0.0/0", destination_port_range: -1, access: Allow, priority: 106,direction: Outbound } 
- { name: DNS_UDP_IN,  protocol: Udp, source_address_prefix: "0.0.0.0/0", destination_port_range: 53, access: Allow, priority: 107,direction: Inbound }
- { name: DNS_UDP_OUT,  protocol: Udp, source_address_prefix: "0.0.0.0/0", destination_port_range: 53, access: Allow, priority: 108,direction: Outbound }
- { name: custom_UDP,  protocol: Udp, source_address_prefix: "0.0.0.0/0", destination_port_range: 8285, access: Allow, priority: 109,direction: Inbound }
- { name: custom_TCP1_IN, protocol: Tcp, source_address_prefix: "0.0.0.0/0", destination_port_range: 1000-65535, access: Allow, priority: 110,direction: Inbound }
- { name: custom_TCP1_OUT, protocol: Tcp, source_address_prefix: "0.0.0.0/0", destination_port_range: 1000-65535, access: Allow, priority: 111,direction: Outbound }
---------------------------

- name: wait when instance become ready to use
  wait_for:
   host: '{{ azure_vm.public_dns_name }}'
   port: "22"
   delay: "60"
   timeout: "320"
   state: "started"

Create a cloud-init script to set the hostname of a Linux VM
https://docs.microsoft.com/en-us/azure/virtual-machines/linux/using-cloud-init#create-a-cloud-init-script-to-set-the-hostname-of-a-linux-vm

Azure/azure-quickstart-templates
https://github.com/Azure/azure-quickstart-templates/tree/master/ansible-advancedlinux

-------------
- name: "Create BIG-IP Virtual Machines"
  shell: >
    /usr/local/bin/azure vm create
    --resource-group {{resource_group}}
    --name {{ node_name }}
    --location {{loc}}
    --vm-size {{vm_size}}
    --nic-names "{{node_name}}-pubnic01","{{node_name}}-privnic01"
    --storage-account-name {{storage_account}}
    --storage-account-container-name "{{storage_container}}"
    --admin-username {{bip_admin}}
    --admin-password {{bip_passwd}}
    --image-urn {{image_urn}}
    --plan-name {{plan_name}}
    --plan-publisher {{plan_publisher}}
    --plan-product {{plan_product}}
    --os-type {{os_type}}
    --custom-data "{{ lookup('template', tp_path) }}"
  register: vm_create_result
  tags: vmonly

- debug: 
    msg: "VM Creation Results: {{vm_create_result}}"
   ----------------------------- 
