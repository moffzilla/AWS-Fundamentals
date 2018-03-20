# AWS_Fundamentals
Automate the deployment of a Web Server with AWS EC2 and ELB 

This project proposes two tracks

1.- AWS CloudFormation
 
	Under "~/CloudFormation"

2.- Ansible + Containerized Apache


	- Make sure resources as the AMI image, SSH Keys, Security Groups referenced in the artifacts exists in the selected region
	This project defaults region US-West-2 (Oregon)

	This is a simple playbook for Provisioning an AWS instance and Installing Docker-CE and Apache, inlcuding recommended packages.
        Adding a secondary HDD hosting Apache default Document Roots with a customized default Welcome Page

Requirements / Tested :

ansible 2.1.1.0

Python 2.7.12+

Amazon Web Services Library boto3 & AWS CLI

You’ll need AWS CLI & this Python module installed on your control machine. Boto can be installed from your OS distribution or python’s using the pip command, install the AWS CLI and Boto3:

'pip install awscli boto3 -U --ignore-installed six'”.

AWS AIM Credentials with enough rigths for launching VMS and of course, if you reference a resource in AWS, such as a Security Group, make sure that the SG exists and it is properly configured, etc.

Make sure you do:

Make sure you can SSH locally with ubuntu (you may need to add your pub key content into the '~/.ssh/authorized_keys')

Disable host checking '/etc/ansible/ansible.cfg' 'host_key_checking = False'

Update the Inventory as follows:
'/etc/ansible/host' 'localhost ansible_connection=local'

Install the 'moffzilla.docker' AKA 'ADC' Role

ansible-galaxy install -r requirements.yml

( More information at https://github.com/moffzilla/ADC )

Execute (Generic)

'export AWS_ACCESS_KEY_ID=[your key]'

'export AWS_SECRET_ACCESS_KEY=[your secret]'

'ansible-playbook Ansible/ec2_Apache.yml -vvvv --user=ubuntu'

Wait for the plays to complete


 	

The following tools are also included for resetting your enviroment


To terminate any AWS Instance created (it requires you to have installed aws cli)
A) To remove all the Machines execute Script

'./terminate_all_instances.py' 

B) To remove an specific machine execute Script

'./list_instances.py'

'./terminate_instances.py [instance-id]'

C) Manually by AWS CLI

'aws ec2 describe-instances | grep InstanceId'

'aws ec2 terminate-instances --instance-ids [i-id]'