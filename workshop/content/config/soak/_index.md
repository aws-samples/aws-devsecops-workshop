+++
title = "Soak Testing Environment"
date = 2020-05-29T14:15:42+01:00
weight = 40
chapter = true
pre = "<b> </b>"
+++

We confugred AWS Config rules in our test environment, which represent our ideal configuration settings. The current rule we are using, `vpc-default-security-group-closed`, checks that the default security group of any VPC does not allow inbound or outbound traffic. If we navigate to the [AWS Config console](https://eu-west-1.console.aws.amazon.com/config/home?region=eu-west-1&awsc-custsat-override=promptUser#/dashboard) we can see our non-compliant rule:

![non-compliant](/images/non-compliant.png)

Our default security group is too permissive. Let's close it down. 
Fisrt, click on the security group ID to go to the VPC Management Console. The default security groups looks something like this:

![compliant](/images/default-sg.png)

Click on "Edit inbound rules" and delete the rule. After this, do the same for the Outbound rules. Going back to the Config console, click on "Re-evaluate" and watch the rule become compliant!

![compliant](/images/compliant.png)

We are now ready to approve our commit to production.

![approve](/images/approve.png)