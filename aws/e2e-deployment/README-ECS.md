## Step by step guide - GitHub, CodeBuild, CodeDeploy and ECS

All of AWS services in this tutorial should be in the same region Singapore (`ap-southeast-1`).

## Pre-requisites
- Github Account
- You have cloned this repo locally: [https://github.com/ardydedase/devops](https://github.com/ardydedase/devops).
Make sure that it is up-to-date by pulling the latest updates from GitHub.
- You have forked this repo to your GitHub account: [https://github.com/ardydedase/sample-flask-docker](https://github.com/ardydedase/sample-flask-docker).
- AWS Account
- AWS EC2 Key Pair. [Follow this tutorial](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-key-pairs.html#having-ec2-create-your-key-pair) and take note of your Key Pair.

## Step by step guide - Create an ECS Stack

This is an application of infrastructure as code. We are using the `ecs-cf.yml` as the Infrastructure Code to describe ECS stack that we want to provision.

1. Login to your AWS Account and open [AWS CloudFormation](https://console.aws.amazon.com/cloudformation). 

1. Click the `Create stack` button to create a new AWS ECS stack using Cloudformation (Infrastructure as Code).

1. Keep the `Template is ready` option and select the `Upload a template file` option.

1. Click the `Choose file` button. Locate the `ecs-cf.yml` file witiin the `aws` folder in the [devops repository](https://github.com/ardydedase/devops) specified in the Pre-requisites section. It can be found in the `aws` folder of the repo.

1. Click the `Next` button.

1. In the `Specify stack details` page, enter your Stack name e.g. `ECS-stack-demo` and choose `t2.micro` as your InstanceType. Keep the rest of the fields to their default value.

1. In the `Configure stack options` page, click `Next`.

1. In the `Review` page, scroll all the way the to the bottom of the page. Tick the acknowledgement tickbox and click `Create stack`.

1. Wait for the Status to be completed.

1. Once the status is completed, open the `Outputs` tab and take note of the `ECSRole` and `VpcId` values. Copy and paste them for use later on.

1. Go to the [ECS page](https://ap-southeast-1.console.aws.amazon.com/ecs/home) and click on the ECS cluster that you have created.

1. Open the Amazon ECR -> Repositories page.

1. Click `Create a repository`. Set the repository name to `sample-flask`. Choose `Mutable` under `Image tag mutability`, then proceed to `Create repository`. This will create a docker image URI placeholder in your repository.

1. Copy the URI of the ECR repository that you have created.

1. Edit the `buildspec.yml` file in the root folder of the cloned [sample-flask-docker](https://github.com/ardydedase/sample-flask-docker) repo.

1. In the `buildspec.yml`file, under the `pre_build` -> `commands` section, replace the value of `REPOSITORY_URI` to your created ECR repository URI.

1. Commit your changes to the `buildspec.yml` file.

## Step by step guide - Setup your Continuous Deployment pipeline

1. Click the `Create pipeline` button. Enter your Pipeline name and your Role name. Click `Next`.

1. In the `Add source stage`, choose Github as the `Source provider`. Click `Connect to GitHub`, you should get the message: "You have successfully configured the action with the provider".

1. Choose the `sample-flask-docker` repository that you have forked in GitHub. Set Branch to master.

1. Keep the GitHub webooks as your Change detection option and click `Next`.

1. In the `Add build stage`, choose `AWS CodeBuild` as your Buld provider. Choose Singapore as `Region`. Click the `Create project` button, 

1. 


Notes

Make sure that the ECS cLuster and load balancer exist first

note the role name

create a cluster first

add role to ECR

Attach policy

privilege mode

https://github.com/aws/aws-codebuild-docker-images/issues/164#issuecomment-460324202


https://docs.aws.amazon.com/codebuild/latest/userguide/sample-docker-custom-image.html#sample-docker-custom-image-files

choose bridge port

setup the security groups

Security Group with description "ECS Allowed Ports"

Choose the security gropu of your load balancer

vpc-0e841d34766e1ac4e


After creating the ECS cluster - take note of the VPC
Load balancer should have the same VPC and security Group