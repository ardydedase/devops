# Puppet on EC2

Infrastructure as code in practice using AWS CloudFormation and Puppet.

## Pre-requisites
- Install Cygwin
- Create Keypair. Take note of the name of the keypair.

## Create your Puppet Master VM on AWS


## References

- https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-init.html
- Troubleshooting cf-init: https://www.reddit.com/r/aws/comments/6a9uk6/cloudformation_having_trouble_with/
- Setting up Putty: https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/putty.html

## Notes

Check cf-init output:

```
cat /var/log/cloud-init-output.log
```