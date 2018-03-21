# AWS_Fundamentals
Automate the deployment of a Web Server with AWS EC2 and ELB 

This project proposes two tracks

1.- AWS CloudFormation
 
	Under "~/CloudFormation"

Execute:

	aws cloudformation create-stack --stack-name mapache-stack --template-url https://s3-us-west-2.amazonaws.com/awsfundamentalsrepo/aws-cloudformation-apache-server-template.json

You can replace the following default settings:

	KeyName": "generic-cloud-wk"
	
	AnsibleRepository": https://github.com/moffzilla/AWS-Fundamentals"
	
	AnsiblePlaybook: "CloudFormation/CF_Apache.yml"
	

You can also create the stack at the CloudFormation Console

Remove:

	aws cloudformation delete-stack --stack-name mapache-stack
	


2.- Ansible + Docker Apache

	Under "~/Ansible"

This is a simple playbook for Provisioning an AWS instance and Installing Docker-CE and Apache, 
Adding a secondary HDD for hosting Apache default Document Roots with a customized default Welcome Page.
Deploying Apache as a Docker Container.

Execute:

	ansible-playbook Ansible/ec2_Apache.yml -vvvv --user=ubuntu
	
Remove: 
	
	'./terminate_all_instances.py' 


General Requirements:

- Make sure resources as the AMI image, SSH Keys, Security Groups referenced in the artifacts exists in the selected region.
- You have permissions for accessing S3 resources, createstacks and to access any other required AWS resource.
- This project defaults region US-West-2 (Oregon) & uses Ubuntu 16.04 guess OS.
- You’ll need AWS CLI & this Python module installed on your control machine. Boto can be installed from your OS distribution or python’s using the pip command, install the AWS CLI and Boto3:

	'pip install awscli boto3 -U --ignore-installed six'”.

- AWS AIM Credentials with enough rigths for launching VMs, if you reference a resource in AWS, such as a Security Group, make sure that the objetc exists and it is properly configured, etc.

- Before executing Ansible Playbook make sure you have access to AWS by exporting or configuring your 
    AWS_ACCESS_KEY_ID
    AWS_SECRET_ACCESS_KEY
    AWS Region

- SW Requirements / Tested :

	ansible 2.1.1.0
	Python 2.7.12+
	Amazon Web Services Library boto3 & AWS CLI
	Ansible 'moffzilla.docker' AKA 'ADC' Role (https://github.com/moffzilla/ADC)

Ansible Specific Requirements :
	
- Make sure you can SSH locally with ubuntu (you may need to add your pub key content into the '~/.ssh/authorized_keys')
- Disable host checking '/etc/ansible/ansible.cfg' 'host_key_checking = False'
- Update the Inventory as follows:
	'/etc/ansible/host' 'localhost ansible_connection=local'
-Install the 'moffzilla.docker' AKA 'ADC' Role
	ansible-galaxy install -r requirements.yml




 	
3.- Appendix - Tools:

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
