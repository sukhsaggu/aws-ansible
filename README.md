Using Ansible with AWS
======================

Ansible control machine is running Mac OS 10.15.1

Prerequisites
-------------

* AWS named profile which has been configured on the ansible control machine
* Security group already setup to allow incoming ssh from any ip
* Keypair already created and downloaded to the ansible control machine. Keypair name is referenced in the playbook

Provision a basic VM
---------------------

Basic no frills playbook to provision a vm.
Playbook run-time : ~ 3mins

This playbook will:

1. Launch an ec2 rhel instance
2. Connect via ssh to the public dns name of the new instance
3. Gather facts on the instance
4. Reboot the instance
5. Terminate the instance

* `<aws_named_profile>` ***value*** =  name of the 'aws named profile'. e.g user-01@awsaccount. This profile should be stored in ~/.aws/credentials
* `<ansible_ssh_private_key_file>` ***value*** = path to private key. e.g ~/aws_keys/my_key.pem

>ansible-playbook launch_aws_ec2_rhel.yml --extra-vars '{"aws_named_profile":"***value***","ansible_ssh_private_key_file":"***value***" }'
