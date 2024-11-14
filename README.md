# Day 2 Project: Build a Simple CI Pipeline with Jenkins
Objective: Today's project is to set up a simple CI (Continuous Integration) pipeline using Jenkins on Amazon Linux. This pipeline will automatically pull code from a GitHub repository and run a basic shell script as a "build step."

## Project Requirements:
Amazon Linux: You'll use Amazon Linux to install and configure Jenkins.
Jenkins setup: Install Jenkins, configure it as a service, and make it accessible from a web browser.
Simple CI job: Set up a Jenkins job that:
Pulls code from a GitHub repository.
Executes a basic shell script (e.g., a script that prints "Hello World!" for now).

## Steps to Implement:
Prepare the Amazon Linux environment:
- Start a fresh Amazon Linux instance (or use the one from yesterday).
- Ensure that git is installed.
- Install Jenkins:
    - Add the Jenkins repository to yum and import its GPG key.
    - Install Jenkins and Java (required to run Jenkins).
    - Start and enable the Jenkins service.
- Configure Jenkins Web Interface:
    - Open port 8080 on the firewall to allow access to Jenkins.
    - Access the Jenkins interface through the browser to complete the initial setup.
- Create a Simple CI Job:
    - Create a GitHub repository (or use an existing one) and add a basic shell script that prints "Hello World!"
    - In Jenkins, create a new Freestyle project that:
        - Pulls code from the GitHub repository.
        - Runs the shell script.

# Solution

Firstly I spun up an t2.medium EC2 instance using Amazon Web Services and configured the security group to have inbound rules to allow SSH access on port 22 and allow inbound access on port 8080 for Jenkins. I then SSH into the instance and installed the pre-requisites using the following;

## Installing git

```
sudo yum update -y
sudo yum install git -y
```

## Installing Jenkins

```
sudo wget -O /etc/yum.repos.d/jenkins.repo \
    https://pkg.jenkins.io/redhat-stable/jenkins.repo

sudo rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io-2023.key

sudo yum upgrade

sudo dnf install java-17-amazon-corretto -y

sudo yum install jenkins -y

sudo systemctl enable jenkins

sudo systemctl start jenkins
```

I then created the bash script and pushed it to the git repository. Thereafter, I created a new Jenkins freestyle job where I configured the git repository and added the build step:

```
bash hello-world.sh
```

Once this was done, I ran the job which was successful with the following output;

![alt text](<Screenshot 2024-11-14 154108.png>)