## Prepare tools
add this lines to ansible config:
```bash
gathering = smart
fact_caching = jsonfile
fact_caching_connection = facts_cache.cache
fact_caching_timeout = 7200
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
