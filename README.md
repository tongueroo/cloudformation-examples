# CloudFormation Examples

These are some very basic raw CloudFormation template examples.  This examples are part of a blog tutorial.

1. [A Simple Introduction to AWS CloudFormation Part 1: EC2 Instance](https://medium.com/boltops/a-simple-introduction-to-aws-cloudformation-part-1-1694a41ae59d)
2. [A Simple Introduction ot AWS CloudFormation Part 2: EC2 Instance and Route53](https://medium.com/boltops/a-simple-introduction-to-aws-cloudformation-part-2-d6d95ed30328)
3. [A Simple Introduction to AWS CloudFormation Part 3: Updating a Stack](https://medium.com/boltops/a-simple-introduction-to-cloudformation-part-3-updating-a-stack-6fe2bb3931a9)
4. [A Simple Introduction to AWS CloudFormation Part 4: Change Sets = Dry Run Mode](https://medium.com/boltops/a-simple-introduction-to-cloudformation-part-4-change-sets-dry-run-mode-c14e41dfeab7)


## Commands from Tutorials

### Tutorial 1

```bash
aws cloudformation create-stack --template-body file://templates/single_instance.yml --stack-name single-instance --parameters ParameterKey=KeyName,ParameterValue=tutorial ParameterKey=InstanceType,ParameterValue=t2.micro
```

### Tutorial 2

```bash
aws cloudformation create-stack --template-body file://templates/single_instance.yml --stack-name --stack-name route53-$(date +%s) --parameters ParameterKey=KeyName,ParameterValue=tutorial ParameterKey=InstanceType,ParameterValue=t2.micro ParameterKey=HostedZoneName,ParameterValue=sub.tongueroo.com. ParameterKey=Subdomain,ParameterValue=testsubdomain

aws cloudformation create-stack --template-body file://templates/instance_and_route53.yml --stack-name route53-$(date +%s) --parameters file://parameters/instance_and_route53.json
```

### Tutorial 3

```bash
$ aws cloudformation create-stack --stack-name example --template-body file://templates/single_instance.yml --parameters file://parameters/single_instance.json

$ aws cloudformation update-stack --stack-name example --template-body file://templates/instance_and_route53.yml --parameters file://parameters/instance_and_route53.json

aws cloudformation update-stack --stack-name example --template-body file://templates/single_instance.yml --parameters file://parameters/single_instance.json
```

### Tutorial 4

```bash
$ aws cloudformation create-stack --stack-name example --template-body file://templates/single_instance.yml --parameters file://parameters/single_instance.json

$ aws cloudformation create-change-set --stack-name example --template-body file://templates/instance_and_route53.yml --parameters file://parameters/instance_and_route53.json --change-set-name changeset-1

$ aws cloudformation describe-change-set --stack-name example --change-set-name changeset-1 | jq '.Changes[]'

$ aws cloudformation execute-change-set --stack-name example --change-set-name changeset-1
```


