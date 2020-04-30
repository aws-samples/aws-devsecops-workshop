+++
title = "Enforcing Compliance"
date = 2020-04-15T14:34:35+01:00
weight = 40
chapter = true
pre = "<b> </b>"
+++

The flexible, dynamic nature of the AWS cloud gives developers and admins the flexibility to launch, configure, use, and terminate processing, storage, networking, and other resources as needed. In any fast-paced agile environment, security guidelines and policies can be overlooked in the race to get a new product to market before the competition.

Imagine that you had the ability to verify that existing and newly launched AWS resources conformed to your organization’s security guidelines and best practices without creating a bureaucracy or spending your time manually inspecting cloud resources.

{{% notice tip %}}
AWS Config is a service that enables you to assess, audit, and evaluate the configurations of your AWS resources. Config continuously monitors and records your AWS resource configurations and allows you to automate the evaluation of recorded configurations against desired configurations. With Config, you can review changes in configurations and relationships between AWS resources, dive into detailed resource configuration histories, and determine your overall compliance against the configurations specified in your internal guidelines. This enables you to simplify compliance auditing, security analysis, change management, and operational troubleshooting.
{{% /notice %}}

![AWS Config](https://d1.awsstatic.com/Products/product-name/diagrams/product-page-diagram-Config_how-it-works.bd28728a9066c55d7ee69c0a655109001462e25b.png)

AWS Config is designed to help you assess compliance with your internal policies and regulatory standards by providing you visibility into the configuration of your AWS resources as well as third-party resources, and evaluating resource configuration changes against your desired configurations on a continuous basis.

You can use AWS Config as your framework for creating and deploying governance and compliance rules across your AWS accounts and regions. You can codify your compliance requirements as AWS Config rules and author remediation actions using AWS Systems Manager Automation documents and package them together within a conformance pack that can be easily deployed across an organization. Therefore, using AWS Config, you can automate assessment of your resource configurations and resource changes to help you ensure continuous compliance and self-governance across your AWS infrastructure.