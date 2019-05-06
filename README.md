##### Project Title

This project is to create two instances on AWS infrastructure in two different AZ in a VPC 

##### Prerequisites

## Required Software’s to install on controlling machine

* To integrate and run the build 
  - Jenkins 
* To create infra on AWS Cloud 
  - Terraform 
* To configure created AWS instances create by terraform 
  - Ansible 
* To setup the encrypted password for IAM user 
  - Keybase 
* To create tomcat container on AWS  
  - Docker
* To perform all above action 
- AWS Account

#### Installing

## Step to Install the Applicaiton 

- Create directory for as Anisble and Terraform and place the site.yml and main.tf
- Create directory in Terraform for your AWS secrete key, access key and perm file.
- Create a shell script in Ansible directory to create invertory.ini file from terraform output.
- Create pipeline job in Jenkins and copy the Jenkins file content in pipeline tab.

# Necessary changes in Jenkinsfile
- change the git repo path
- change the other path according to your setup. 

# Necessary changes for Terraform file
- Create a variable file for aws_access_key, aws_secret_key and private_key_path.
- Install keybase on controlling machine and provide keybase user in pgp_key in terraform file.

## Build Flow

1. Applicaiton checkout from GIT repo.
2. Build the application with maven.
3. Create infrastructure on AWS as listed in main.tf file.
4. Redirect aws_instance_public_dns to aws_dns_name.txt file.
5. Redirect the password output to home directory of keybase user.
6. Shell scripting call to generate invertory.ini file for hosts, mentioned in aws_dns_name.txt
7. Ansible playbook call to configure hosts for Docker, Tocat Apache installation.
8. Catch build FAILURE

## Authors

Arun Gaurav - arun.gaurav1989@gmail.com
