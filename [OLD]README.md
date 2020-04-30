# DevSecOps on AWS

DevSecOps covers security of and in the CI/CD pipeline, including automating security operations and auditing. The goals of DevSecOps are to:

- Embed security knowledge into DevOps teams so that they can secure the pipelines they design and automate.
- Embed application development knowledge and automated tools and processes into security teams so that they can provide security at scale in the cloud.

To embed the DevSecOps discipline in the enterprise, AWS customers are automating CAF controls using a combination of AWS and third-party solutions.

- AWS solutions: Amazon Cloudwatch Alarms,  AWS CloudTrail,  Amazon CloudWatch Events, AWS Lambda, AWS Config
- Third-party solutions: Dome9, Evident.IO


## Tales from DevSecOps at AWS Podcast
You can't buy it. It's not a thing you install and everything will be fine.
DevOps where Security is a requirement. Fundamentally helping people ship securetly
Capability that an organisation has to ship and move fast securely
Culture and technology make it come to life

#### Outcome
Accelerating the SecOps teams to keep up with the development team
How fast do you react and detect vulnerabilities
Event driven architectures. As long as a team is ready, it triggers the workload to the team after.
Security people are an order of magnitude smaller than developer teams
Going from security is the "department of no" to security being an enabler

#### Assessment
Landing Zones. Security code in another account, and have a look at your Org structure.
Cross functional team working together
Executive sponsorship. CEO, CISO, CTO
Iterative journey
Pick smaller workloads, demonstrate what good looks like

#### Journey
Developers are not the experts of what is secure. Security by default - if the developer gets his code through the pipeline it is no longer his responsibility
Feedback in the IDE, build, test. Check against infrastructure, networking, IAM, app code. Deploy.
Automation of the development and deployment pipeline.
Config and config rules for detection, WAF are in place for the SDL to move as security as possibly post deployment.

Cryptographically verify the test to prove it was testing. Accountability. Developer commits code. Code goes through tests. If tests pass (security testing as part of functional testing as early as possible). If you sign those tests, when audit teams come you can prove that test has been applied. 
Allows for day by day auditing. Doesn't need to happen twice a year. Audit comunity gets the posture of the environment at any point in time. On-demand audit model.

Security sets the barriers of what's good. Config is great to set that holistically. Codify principals you want to exist in all accounts and application. Feedback direct to the developers.
SCPs will further enforce what people can and cannot do in an organisation. Security as an enabler function for developers. Work together rather than in opposition with developers. Same language together: code. 
Scaling mechanism for the security, and clarity of thought.
Provable security and consistency.

Ephemeral compute (p.e. discard containers every 24h hours and rebuild them)
Minimizing ammount of time deployed
ECR scan on commit

Help deliver a great experience to customers and help them take care of their business.

#### At AWS
Security is job 0
Very strong culture of security across everybody who works here
Partially because our non-security leaders say it's an important thing
Because it's not coming just from the security org, it's important to everyone in the business. CIO, CTO, COO want org to go fast but security is an important part of that
What are the things that we need to build across people, culture and technology that help us deliver security at speed

#### Skills
Security specialist
 - Face a rapidly changing technology landscape
 - Prepared to dive deeper in AWS and take the Security Certification Specialty and learning path
 - How would codified security look like in an envirnoment you own?
 - Start with Python. Lambda, config, other SDKs
 - https://awssecworkshops.com/

Everyone
 - Get in the mindset

## Tools and Steps for this Workshop

### 0. [cfn-validate-template](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/using-cfn-validate-template.html)
The aws cloudformation validate-template command is designed to check only the syntax of your template. It does not ensure that the property values that you have specified for a resource are valid for that resource. Nor does it determine the number of resources that will exist when the stack is created.


### 1. [cfn_nag](https://github.com/stelligent/cfn_nag)

The cfn-nag tool looks for patterns in CloudFormation templates that may indicate insecure infrastructure. Roughly speaking it will look for:

- IAM rules that are too permissive (wildcards)
- Security group rules that are too permissive (wildcards)
- Access logs that aren't enabled
- Encryption that isn't enabled
- Password literals


### 2. [taskcat](https://github.com/aws-quickstart/taskcat)

**taskcat** is a tool that tests AWS CloudFormation templates. It deploys your AWS CloudFormation template in multiple AWS Regions and generates a report with a pass/fail grade for each region. You can specify the regions and number of Availability Zones you want to include in the test, and pass in parameter values from your AWS CloudFormation template. taskcat is implemented as a Python class that you import, instantiate, and run.

https://aws.amazon.com/blogs/infrastructure-and-automation/up-your-aws-cloudformation-testing-game-using-taskcat/

### 3. [DevSecOps using CodePipeline](https://aws.amazon.com/blogs/devops/implementing-devsecops-using-aws-codepipeline/)

![Pipeline](https://d2908q01vomqb2.cloudfront.net/7719a1c782a1ba91c031a682a0a2f8658209adbf/2017/03/23/demo_pipeline1.png)

### 4. [Continuous integration and evaluation of security controls](https://aws.amazon.com/blogs/security/how-to-manage-security-governance-using-devops-methodologies/)

```
Scenario: User is starting an instance in a VPC
`
“Given that I am logged in to the AWS Console
and I have permissions to start an instance in a VPC
When I try to start an instance
and the AMI is not tagged as hardened
Then it is denied” [Preventative]

“Given that I am logged into the AWS console
and I have permission to start an instance in the VPC
When I try to start an instance 
and the AMI is not tagged as hardened
Then an email is sent to the Security Operations Team.” [Responsive]

“Given that I am logged into the AWS Console
and I have permission to start an instance in the VPC
When I try to start and instance that is tagged as hardened
Then the instance starts.” [Allowed]
```

After you write multiple action statements and scenarios supporting the user story (both positive and negative), you can write them up as a runbook, an AWS Config rule, or a combination of both as required.

The second example acceptance criteria above would need to be written as a runbook, as it’s a responsive control. You wouldn’t want to generate a stream of emails to your security operations manager to validate that it’s working.

The other two examples could be written as AWS Config rules using a call to the iam:simulate-custom-policy API, since they are related to preventative controls. An AWS Config rule allows your entire account to be continuously evaluated for compliance, essentially evaluating your control adherence on a <15min basis, rather than from a yearly audit.

Committing those runbook and AWS Config rules to a central code repository fosters the agility of the controls. In the case of runbooks, you may want to adopt a light-weight markup format, such as markdown, that you are able to check in like code. The defined controls can then sit in a CI/CD pipeline, allowing the security controls to be as agile as your pace of innovation.

#### 4.1. [AWS Config](https://aws.amazon.com/config/)
You can use AWS Config as your framework for creating and deploying governance and compliance rules across your AWS accounts and regions. You can codify your compliance requirements as AWS Config rules and author remediation actions using AWS Systems Manager Automation documents and package them together within a conformance pack that can be easily deployed across an organization. Therefore, using AWS Config, you can automate assessment of your resource configurations and resource changes to help you ensure continuous compliance and self-governance across your AWS infrastructure.

#### 4.2. [Amazon Inspector](https://aws.amazon.com/inspector/?nc2=h_ql_prod_se_in)
Amazon Inspector is an API-driven service that analyzes network configurations in your AWS account and uses an optional agent for visibility into your Amazon EC2 instances. This makes it easy for you to build Inspector assessments right into your existing DevOps process, decentralizing and automating vulnerability assessments, and empowering your development and operations teams to make security assessments an integral part of the deployment process.


### 5. [The AWS Cloud Adoption Framework Security Perspective](https://d1.awsstatic.com/whitepapers/AWS_CAF_Security_Perspective.pdf)

In an environment where infrastructure is code, security must also be treated as code. The Security Operations component provides a means to communicate and operationalize the fundamental tenets of security as code:

- Use the cloud to protect the cloud.
- Security infrastructure should be cloud-aware.
- Expose security features as services using the API.
- Automate everything, so that your security and compliance can scale.

To make this governance model practical, lines of business often organize as DevOps teams to build and deploy infrastructure and business software. You can extend the core tenets of the governance model by integrating security into your DevOps culture or practice; which is sometimes called DevSecOps. Build a team around the following principles:

- The security team embraces DevOps cultures and behaviors.
- Developers contribute openly to code used to automate security operations.
- The security operations team is empowered to participate in testing and automation of application code.
- The team takes pride in how fast and frequently they deploy. Deploying more frequently, with smaller changes, reduces operational risk and shows rapid progress against the security strategy.

Integrated development, security, and operations teams have three shared, key missions.
- Harden the continuous integration/ continuous deployment tool chain.
- Enable and promote the development of resilient software as it traverses the
tool chain.
- Deploy all security infrastructure and software through the tool chain.

Determining the changes (if any) to current security practices will help you plan a smooth AWS adoption strategy.

![CAF](https://d2908q01vomqb2.cloudfront.net/22d200f8670dbdb3e253a90eee5098477c95c23d/2018/11/15/security-controls-01.jpg)



### [Walkthrough: Building a Pipeline for Test and Production Stacks](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/continuous-delivery-codepipeline-basic-walkthrough.html)
This walkthrough builds a pipeline for a sample WordPress site in a stack. The pipeline is separated into three stages. Each stage must contain at least one action, which is a task the pipeline performs on your artifacts (your input). A stage organizes actions in a pipeline. CodePipeline must complete all actions in a stage before the stage processes new artifacts, for example, if you submitted new input to rerun the pipeline.

By the end of this walkthrough, you'll have a pipeline that performs the following workflow:

1. The first stage of the pipeline retrieves a source artifact (an AWS CloudFormation template and its configuration files) from a repository.
You'll prepare an artifact that includes a sample WordPress template and upload it to an S3 bucket.

2. In the second stage, the pipeline creates a test stack and then waits for your approval.
After you review the test stack, you can choose to continue with the original pipeline or create and submit another artifact to make changes. If you approve, this stage deletes the test stack, and then the pipeline continues to the next stage.

3. In the third stage, the pipeline creates a change set against a production stack, and then waits for your approval.
In your initial run, you won't have a production stack. The change set shows you all of the resources that AWS CloudFormation will create. If you approve, this stage executes the change set and builds your production stack.


## Resources

aws-codebuild-samples: https://github.com/aws-samples/aws-codebuild-samples

Jason Giles example: https://github.com/JasonAGiles/aws-cloudformation-pipeline-example

Paul Duvall example: https://stelligent.com/2019/11/27/run-aws-cloudformation-tests-from-codepipeline-using-taskcat/

Up your AWS CloudFormation testing game using TaskCat: https://aws.amazon.com/blogs/infrastructure-and-automation/up-your-aws-cloudformation-testing-game-using-taskcat/

Using AWS Systems Manager Parameter Store Secure String parameters in AWS CloudFormation templates: https://aws.amazon.com/blogs/mt/using-aws-systems-manager-parameter-store-secure-string-parameters-in-aws-cloudformation-templates/

git-secrets: https://github.com/awslabs/git-secrets
CodeGuru Reviwerer
