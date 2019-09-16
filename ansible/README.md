## Prepare tools
add this lines to ansible config:
```bash
gathering = smart
fact_caching = jsonfile
fact_caching_connection = facts_cache.cache
fact_caching_timeout = 7200
```
> Fill variables for Ansible
> ansible/group_vars/all/vars.yml
```yaml
--                                                                                                                                                                                          
SSH_KEY_NAME: mtiurin_aws_devops           # Name of your ssh key                                                                                                                                                            
VPC_NAME: mtiurin-vpc                      # Name of your VPC
VPC_NET: 10.1.100.0/16                     # VPC capacity                                                                                                                                                  
VPC_SUBNET: 10.1.100.0/24                  # Subnet1 capacity
VPC_SUBNET2: 10.1.101.0/24                 # Subnet2 capacity                                                                                                                                                  
AWS_REGION: eu-central-1                                                                                                                                                                     
AWS_ZONE1: eu-central-1a                                                                                                                                                                     
AWS_ZONE2: eu-central-1c                                                                                                                                                                     
SECURITY_GROUP_NAME: mtiurin_aws_devops                                                                                                                                                      
EC2_INSTANCE_NAME: mtiurin_aws_devops_1                                                                                                                                                      
#BASE_AMI: ami-0cfac31dd01a5f898                                                                                                                                                             
BASE_AMI: ami-026d3b3672c6e7b66            # AMI from whitch OUR should be nested (RH based please!)                                                                                                                                                  
TARGET_AMI: mtiurin_aws_devops                                                                                                                                                               
EC2_TYPE: t2.micro                         # instance type. (only for AMI creation)
EC2_PUBLIC: yes                                                                                                                                                                              
HOME: "{{ lookup('env','HOME') }}"         # Variables will be used to creat ssh key from your key in ~/.ssh/id_rsa                                                                                                                                                  
USER: "{{ lookup('env','USER') }}"         # Variables will be used to creat ssh key from your key in ~/.ssh/id_rsa                                                                                                                                                 
# OPTIONAL CONFIGS
DNS_ZONE: gridu.aws.griddynamics.net       # Optional (Not used for CloudFormation activity) You could create route53 zone and point your EC2 to it.                                                                                                                                                  
DNS_NAME: prexus                           # hostname in dns zone                                                                                                                                                 
EBS_VOLUME_NAME: "mtiurin_aws_ebs_vol_20g" # Optional EBS mount
ASG_NAME: "mtiurin_aws_asg"                # Scaling Group Name                                                                                                                                                  
IAM_ROLE: ec2_full                         # IAM role
```

## PREPARE AMI:
>Building EC2 instanse, VPC , subnet etc.
* `ansible-playbook ec2.yml`
>Installing Nexus to target EC2 host
* `ansible-playbook -i aws  nexus.yml`
> Deleting previuos AMI , creating AMI image and removing EC2 instance
> Job prints AMI id.
* `ansible-playbook -i aws  ami.yml`
```bash
TASK [ami : NEW AMI IMAGE:] *****************************************************************************************************************************************************************
ok: [localhost] => {
    "ami.results[0].image_id": "ami-099c4428c7f5e6b97"
}
```
