Using Ansible with AWS
======================

Basic, no frills, single file playbooks to provision, run tasks and terminate a vm.

Ansible control machine is running Mac OS 10.15.1

ansible --version  = 2.9.0

Prerequisites
-------------

* AWS named profile which has been configured on the ansible control machine. See https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-profiles.html
* AWS Security group already setup to allow incoming ssh or winrm from any ip
* AWS Keypair already created and downloaded to the ansible control machine. (Keypair name is referenced in the playbook)

Provision a basic VM (Red Hat Enterprise Linux)
-----------------------------------------------

Playbook run-time : ~ 3 mins

This playbook will:

1. Launch an ec2 rhel instance
2. Connect via ssh to the public dns name of the new instance
3. Gather facts on the instance
4. Reboot the instance
5. Terminate the instance

* `<aws_named_profile>` ***value*** =  name of the 'aws named profile'. e.g user-01@awsaccount. This profile should be stored in ~/.aws/credentials
* `<ansible_ssh_private_key_file>` ***value*** = path to private key. e.g ~/aws_keys/my_key.pem

>ansible-playbook launch_aws_ec2_rhel.yml --extra-vars '{"aws_named_profile":"***value***","ansible_ssh_private_key_file":"***value***" }'

Provision a basic VM (Windows Server 2016)
-----------------------------------------------

Playbook run-time : ~ 7 mins

This playbook will:

1. Launch an ec2 windows instance
2. Retrive the windows local admin password
3. Connect via winrm to the public dns name of the new instance
4. Gather facts on the instance
5. Reboot the instance
6. Terminate the instance

* `<aws_named_profile>` ***value*** =  name of the 'aws named profile'. e.g user-01@awsaccount. This profile should be stored in ~/.aws/credentials
* `<key_file_path>` ***value*** = path to private key. e.g ~/aws_keys/my_key.pem

>ansible-playbook launch_aws_ec2_win.yml --extra-vars '{"aws_named_profile":"***value***","key_file_path":"***value***" }'
