+++
title = "Clone Repository"
date = 2019-11-01T16:13:49-07:00
weight = 10
chapter = true
pre = "<b></b>"
+++

1. [Clone](https://help.github.com/articles/cloning-a-repository/) this repository. From your terminal application, execute the following command. This creates a directory named aws-devsecops-workshop in your current directory.

```
git clone https://github.com/aws-samples/aws-devsecops-workshop
```

2. [Create AWS CodeCommit repository](http://docs.aws.amazon.com/codecommit/latest/userguide/getting-started.html#getting-started-create-repo) in your AWS account and [set up AWS CLI](http://docs.aws.amazon.com/codecommit/latest/userguide/how-to-create-repository.html#how-to-create-repository-cli). Name your repository wordpress-cfn. Alternatively, from your terminal application, execute the following command and note the `cloneUrlHttp URL` in the response from the CLI.

```
aws codecommit create-repository --repository-name wordpress-cfn --repository-description "This template installs WordPress with a local MySQL database for storage"
```

3. [Create the local git setup](http://docs.aws.amazon.com/codecommit/latest/userguide/setting-up.html) required to push code to CodeCommit repository and add a new remote. From your terminal application, within the wordpress-dfn directory, execute the following command:

```
git init && git remote add AWSCodeCommit HTTP_CLONE_URL_FROM_STEP_2
```

4. [Install git-secrets](https://github.com/awslabs/git-secrets) and ensure the git repository is scanned for secrets on each commit.

```
git secrets --install
git secrets --register-aws
```

{{% notice tip %}}
git-secrets scans commits, commit messages, and --no-ff merges to prevent adding secrets into your git repositories. If a commit, commit message, or any commit in a --no-ff merge history matches one of your configured prohibited regular expression patterns, then the commit is rejected.
{{% /notice %}}

{{% notice warning %}}
https://github.com/aws-samples/aws-devsecops-workshop/blob/master/wordpress/wordpress-single-instance.yaml
{{% /notice %}}