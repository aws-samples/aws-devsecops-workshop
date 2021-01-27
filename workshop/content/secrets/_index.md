+++
title = "Store Secrets"
date = 2019-10-30T17:50:15-07:00
weight = 15
chapter = true
pre = "<b> </b>"
+++

When using AWS CloudFormation templates to code your infrastructure, you should consider applying best practices to improve the maintainability of your code. Further, these best practices should be augmented by guidelines like those outlined for twelve-factor apps, which are targeted at optimizing applications for continuous deployment. Of these factors, you should note that you should strive for strict separation of configuration information from your code wherever possible, since configuration information will often vary across deployments, while code typically does not. Also, from a code and configuration perspective, you should strive to keep your development and production code as similar as possible because this will aid quick replication of any production issues or bugs.

With AWS CloudFormation, you have several options to avoid storing configuration as constants in your template code, which amounts in most cases to hardcoding runtime configuration details. Instead, you should take advantage of various options for using parameters. Further, you can elicit those parameters from users in the AWS Management Console, or from a separate runtime variable by using a CLI or API call, or by using a parameter file.

```yaml
#
# This snippet of the template accesses stored parameters
# for the database name and passwords.
# A non-secure SSM Parameter for the DB name
# A Secrets Manager Parameter for the master password
#
Parameters:
  DBName:
    Description: The WordPress database name
    Default: "{{resolve:ssm:dbName:1}}"
    Type: String
  DBPassword:
    Description: The WordPress database admin account password
    Default: "{{resolve:secretsmanager:dbPassword}}"
    Type: String
```

In the console, initialise the parameters the Wordpress stack fetches from AWS Systems Manager Parameter Store and AWS Secrets Manager using your CLI.

```bash
aws ssm put-parameter --name dbName --type String --value "WordPressDB"
aws ssm put-parameter --name dbUser --type String --value "DBuser"
aws secretsmanager create-secret --name dbPassword --secret-string DBPassword
aws secretsmanager create-secret --name dbRootPassword --secret-string DBRootPassword
```


AWS Secrets Manager is a service to manage the lifecycle for the secrets used in your organization centrally including rotation, audit, and access control. Secrets Manager helps you meet your security and compliance requirements by enabling you to rotate secrets automatically. Secrets Manager offers built-in integration for MySQL, PostgreSQL, and Amazon Aurora on Amazon RDS that's extensible to other types of secrets by customizing Lambda functions.

AWS Systems Manager Parameter Store provides secure, hierarchical storage for configuration data management, which can include secrets. Data such as database strings, passwords, and license codes can be stored as parameter values. Values stored can be either plain text or encrypted data. You can then reference values by using the unique name specified when creating the parameter. You can reference Systems Manager parameters in your scripts and commands for configuration and automation workflows.

{{% notice tip %}}
Generally speaking, if you only need simple store/retrieve functionality use AWS Systems Manager Parameter Store. If you wants extra functionality, such as lifecycle management and rotation, use AWS Secrets Manager.
{{% /notice %}}

<!-- https://aws.amazon.com/blogs/security/how-to-create-and-retrieve-secrets-managed-in-aws-secrets-manager-using-aws-cloudformation-template/ -->
<!-- https://aws.amazon.com/blogs/mt/using-aws-systems-manager-parameter-store-secure-string-parameters-in-aws-cloudformation-templates/ -->
