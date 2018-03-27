# AWS Fundamentals
This project creates a running EC2 instance meeting the AWS Fundamental Exercise #1 requirements
It provides two alternative "tracks" for accompishing it.

Updates available at https://github.com/moffzilla/AWS-Fundamentals

AWS CloudFormation Track: 

Makes use of AWS CloudFormation templates to create EC2 infrastructure and Ansible for staging new volumes, install Docker and deploy Apache as a container.
	
	EIP Associated with EC2 Instance:**54.191.197.245**

	Public DNS Associated with EC2 Instance:**http://ec2-54-191-197-245.us-west-2.compute.amazonaws.com/**
	
	URL Associated with EC2 Instance:**http://awscf.moffzilla.io**

	Link showing mounted EBS Volume: **http://awscf.moffzilla.io/screen-shot1.png**

	Link showing index.html resides within EBS:**http://awscf.moffzilla.io/screen-shot2.png** 


Ansible Track: 
Makes use of Ansible to create EC2 infrastructure and for staging new volumes, install Docker and deploy Apache as a container.

	EIP Associated with EC2 Instance:**52.42.214.106**

	Public DNS Associated with EC2 Instance:**ec2-52-42-214-106.us-west-2.compute.amazonaws.com**
	
	URL Associated with EC2 Instance:**http://awsansible.moffzilla.io**
	
	Link showing mounted EBS Volume: **http://awsansible.moffzilla.io/screen-shot1.png**

	Link showing index.html resides within EBS:**http://awsansible.moffzilla.io/screen-shot2.png** 


Implementation details and artifacts information for each track below:

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
	


2.- Ansible

	Under "~/Ansible"

Execute:

	'ansible-playbook Ansible/ec2_Apache.yml -vvvv --user=ubuntu'
	
Remove: 
	
	'aws ec2 describe-instances | grep InstanceId' 
	'./terminate_instances.py [instance-id]' 


General Requirements:

- Make sure resources as the AMI image, SSH Keys, Security Groups referenced in the artifacts exist in the selected region.
- You have permissions for accessing S3 resources you may create to replace default ones, createstacks and to access any other required AWS resource.
- You have created a bucket : "awsfundamentalsrepo" and uploaded the stack template : "aws-cloudformation-apache-server-template.json".
- This project defaults region US-West-2 (Oregon) & uses Ubuntu 16.04 guess OS.
- You’ll need AWS CLI installed.
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
	
- You will need installed this Python module & Boto can be installed from your OS distribution or python’s using the pip command, install the AWS CLI and Boto3:

	'pip install awscli boto3 -U --ignore-installed six'”.

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
