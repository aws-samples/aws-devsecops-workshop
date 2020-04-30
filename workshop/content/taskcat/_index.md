+++
title = "Testing a Template"
date = 2020-04-15T14:33:32+01:00
weight = 35
chapter = true
pre = "<b> </b>"
+++

We passed our validate stage! The vpc ID `default-vpc` does not exist. We can leave it out of the security group, as the default works just fine.

[TaskCat](https://github.com/aws-quickstart/taskcat) is an open source tool developed by the AWS Quick Start team to automate the testing of AWS CloudFormation templates. It tests an AWS CloudFormation template by deploying it in multiple AWS Regions simultaneously and generates a report with a pass/fail result for each Region. You can customize the tests through a test config file. TaskCat is implemented in Python and available as a Docker container and pip module.

![Taskcat](https://raw.githubusercontent.com/aws-quickstart/taskcat/master/assets/docs/images/logo.png)

To run the tests, TaskCat requires a configuration file named taskcat.yml. The taskcat.yml file contains two high-level mappings: global and tests. The global mapping defines the global configurations of the project:
 - owner – Project owner’s email address
 - qsname – Name of the project; must be same as the project folder name
 - regions – All the regions where tests need to be executed
 - reporting – To generate test report with logs from each test execution

The tests mapping defines test scenarios that will be performed by TaskCat. You can define multiple test scenarios in the tests mapping, and each test scenario must specify a parameter input file name and an AWS CloudFormation template file name. Optionally, you can define the AWS Regions in which the test needs to be executed. This Region list will override the global Region list. For example, if your AWS CloudFormation template creates AWS resources that are not available in all Regions, you need to override the global Region list and specify only those Regions where those resources are supported.

```yaml
project:
  name: wordpress-single-instance
  regions:
    - eu-west-1
tests:
  default:
    template: wordpress/wordpress-single-instance.yaml
```

TaskCat performs multiple actions, such as template validation, parameter validation, and staging content into an Amazon Simple Storage Service (Amazon S3) bucket, before launching the AWS CloudFormation stack. It launches the stack in the defined Regions, simultaneously. And it regularly polls the AWS CloudFormation stack status to check if the stack creation is finished. After the stack has been successfully created, TaskCat deletes it. How much time TaskCat takes to finish the testing depends on how many tests you have defined in your TaskCat configuration file and how long each stack creation and deletion takes. After the TaskCat run is completed, it generates a report in HTML format in the directory from where you are running the TaskCat command. 

{{% notice tip %}}
To get the best results when testing your templates with TaskCat, it’s helpful to understand three primary files that TaskCat uses: Standard parameter file, Override parameter files and the configuration file. [Take a look](https://aws.amazon.com/blogs/infrastructure-and-automation/a-deep-dive-into-testing-with-taskcat/) at each of these files in more detail, and at how you can use them to create and configure the test cases for your CloudFormation templates.
{{% /notice %}}

![soaktest](/images/soaktest.png)

<!-- https://aws.amazon.com/blogs/infrastructure-and-automation/up-your-aws-cloudformation-testing-game-using-taskcat/ -->
<!-- https://aws.amazon.com/blogs/infrastructure-and-automation/a-deep-dive-into-testing-with-taskcat/ -->