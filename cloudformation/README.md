# Build stack with template
> Stack provision infrastructure and prints nexus URL and external for VPN.
```bash
aws cloudformation create-stack  --template-body file://custom_stack.yml --stack-name >>> INSERT STACK_NAME <<< --parameters ParameterKey=AMI,ParameterValue=>>>INSERT AMI id here<<<
```
> You can check state with:
```bash
aws cloudformation  describe-stack-events --stack-name >>>INSERT STACK_NAME<<<
```

> To check output use:
```bash
aws cloudformation  describe-stacks --stack-name >>>INSERT STACK_NAME<<<
```

> To setup SSH-VPN use sshuttle 
```bash
SSHVPNIP=>>> VALUE OF SSHVPNIP OUTPUT KEY <<< sshuttle --dns -r ec2-user@${SSHVPNIP} -x ${SSHVPNIP}  0/0 || true
```

> Delete stack with:
```bash
aws cloudformation  delete-stack --stack-name >>>INSERT STACK_NAME<<<
```
