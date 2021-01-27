+++
title = "Conclusion and Clean Up"
date = 2019-10-30T17:50:15-07:00
weight = 100
chapter = true
pre = "<b> </b>"
+++

![completed](/images/completed.png)

It's done! We managed to deploy our Wordpress stack making sure we have security in our development pipeline. To get started building your DevSecOps approach, take a step back and ask yourself, “What am I trying to accomplish, and what security controls are needed?”. This step helps you create a focused use case, and from there, you can identify options for security tools, automation requirements, and organizational roles and processes that you need to address. Finally, include an audit, logging, and monitoring solution in your production environment that combines account activity and AWS resources from AWS CloudTrail and AWS CloudWatch with data on security incidents to provide ongoing insights, as well as other controls, such as Identity and Access Management (IAM) and network security.

To cleanup the resources, destroy the CloudFormation template in your account and the CodeCommit repository:

```bash
aws cloudformation delete-stack --stack-name devsecops-wordpress-pipeline
aws codecommit delete-repository --repository-name wordpress-cfn
```