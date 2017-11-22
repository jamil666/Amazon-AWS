# Amazon-AWS
This script create new Amazon AWS EC2 Instance
Need to provide AWS region and Hostname for VM. 
Free Elsatic IP will be assigned automaticaly from EIP list
Need to create UserData file for post install process. File name should be thesame as in power shell script

#!/bin/bash
hostname
yum update -y
yum install -y php nginx
chkconfig nginx on

instance-id=$(curl -s http://169.254.169.254/latest/meta-data/instance-id)

aws configure set aws_access_key_id {your access key}
aws configure set aws_secret_access_key {your secret key}
aws configure set region {your region}

# associate Elastic IP
INSTANCE_ID=$(curl -s http://169.254.169.254/latest/meta-data/instance-id)
ALLOCATION_ID=
aws ec2 associate-address --instance-id $INSTANCE_ID --allocation-id $ALLOCATION_ID --allow-reassociation
