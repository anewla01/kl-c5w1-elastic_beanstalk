# Overview

This document serves as notes, and reflections on a mock situation to deploy a
retail banking application into AWS Elastic Beanstalk.

Business use case: A Retail Bank wants to deploy an application to the cloud
that is fully managed by AWS. In order to achieve this, their source code must
be uploaded to and configured in AWS Elastic Beanstalk.

Tech Stack:

- CICD: Jenkins
- Cloud Infrastructure:
  - Elastic Beanstalk
- Application: Python, Flask App

# Reflections

## Preparation

- What is elastic bean stalk
- What is Jenkins

## EC2 Deploy

- Key Pair -- articulation of what pem files are
- Q:
  - how does one know how to configure the security group wrt to the application
    that is being provided
    - e.g: in the case of jenkins running on this ec2 instance how is it clear
      that this is what is needed?
- CALLOUT: this step is necessary, without we would have no where to provide
  jenkins.

## Installing Jenkins and Connecting Github

- Breakign down Jenkins set commands

```bash
sudo apt update
sudo apt install fontconfig openjdk-17-jre software-properties-common
sudo add-apt-repository ppa:deadsnakes/ppa
sudo apt install python3.7 python3.7-venv
sudo wget -O /usr/share/keyrings/jenkins-keyring.asc https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key
echo "deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc]" https://pkg.jenkins.io/debian-stable binary/ | sudo tee /etc/apt/sources.list.d/jenkins.list > /dev/null;
sudo apt-get update;
sudo apt-get install jenkins;
sudo systemctl start jenkins;
sudo systemctl status jenkins;
```

- Discussion of the permissions that are being provided to jenkins for github
- CALLOUT: Could not update commit status. Message: {"message":"Resource not
  accessible by personal access
  token","documentation_url":"https://docs.github.com/rest/commits/statuses#create-a-commit-status","status":"403"}
  - fine grain permissioning
- TODO: provide screen shot of succesful build

## Deploying Elastic Beanstalk

- IAM Permissioning
  - aws-elasticbeanstalk-service-role
  - ec2
    - AWSElasticBeanstalkWebTier
    - AWSElasticBeanstalkWorkerTier
    - AWSElasticBeanstalkMulticontainerDocker

# Optimizations

- CALLOUT: we deployed code manually to ELB during the initialization phase, but
  this is not in fact connected to Jenkins
  - Additionally shipping code as 3.7 python which is now deprecated () ERROR:
- ERRORS
  - Environment must have instance profile associated with it.
  - 502 Bad Gateway
- CALLOUT: running flask app directly on the ec2 requires additional manual
  effort
  - NOTE: did this manually to verify that ELB env was configured correctly
    - NOTE: would need to properly install python virtual environment e.

REQUIRED: "OPTIMIZATION" section for that answers the question: What are the
benefits of using managed services for cloud infrastructure? What are some
issues that a retail bank would face choosing this method of deployment and how
would you address/resolve them? What are other disadvantages of using elastic
beanstalk or similar managed services for deploying applications?

# Diagram

# Conclusion
