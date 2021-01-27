+++
title = "Clone Repository"
date = 2019-11-01T16:13:49-07:00
weight = 10
chapter = true
pre = "<b></b>"
+++

1. Clone this repository. From your terminal application, execute the following command. This creates a directory named aws-devsecops-workshop in your current directory.

```
git clone https://github.com/aws-samples/devsecops-workshop-on-aws
cd devsecops-workshop-on-aws
```

2. Create AWS CodeCommit repository in your AWS account and set up the AWS CLI. Name your repository wordpress-cfn. Alternatively, from your terminal application, execute the following command and note the `cloneUrlHttp URL` in the response from the CLI.

```
aws codecommit create-repository --repository-name wordpress-cfn --repository-description "This template installs WordPress with a local MySQL database for storage"
pip install git-remote-codecommit
```

3. Create the local git setup required to push code to CodeCommit repository and add a new remote. From your terminal application, within the 'devsecops-workshop-on-aws' directory, execute the following command:

```
git init && git remote add AWSCodeCommit codecommit::eu-west-1://wordpress-cfn
```

4. Install git-secrets and ensure the git repository is scanned for secrets on each commit.

```
git clone https://github.com/awslabs/git-secrets.git
cd git-secrets && make install && cd ..
git secrets --install
git secrets --register-aws
```

5. Push the repository into AWS Code Commit.

```
git push AWSCodeCommit master
```

{{% notice tip %}}
git-secrets scans commits, commit messages, and --no-ff merges to prevent adding secrets into your git repositories. If a commit, commit message, or any commit in a --no-ff merge history matches one of your configured prohibited regular expression patterns, then the commit is rejected.
{{% /notice %}}