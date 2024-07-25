# jenkins
learn abouts jenkins and how to install Jenkins in the ec2 instance 


# Jenkins on AWS EC2

## Overview

Jenkins is an open-source automation server that enables developers to build, test,
and deploy their software in a reliable and efficient manner. It is widely used for
continuous integration (CI) and continuous delivery (CD) practices. This repository
provides a step-by-step guide to installing Jenkins on an Ubuntu EC2 instance on AWS.

## Features of Jenkins

- **Extensible**: With hundreds of plugins in the Update Center, Jenkins integrates with virtually every tool in the CI/CD toolchain.
- **Distributed Builds**: Jenkins can distribute build/test loads to multiple computers.
- **Pipeline**: Provides a way to define a series of steps to be run, either sequentially or in parallel.
- **Easy Installation**: Jenkins can be installed through native system packages, Docker, or even run standalone by any machine with a Java Runtime Environment (JRE) installed.
- **Easy Configuration**: Jenkins is easily set up and configured via its web interface, which includes on-the-fly error checks and built-in help.

## Prerequisites

- **AWS Account**: Ensure you have an active AWS account.
- **EC2 Instance**: An Ubuntu 20.04 LTS EC2 instance.
- **SSH Key**: Your SSH key pair (.pem file) for connecting to the EC2 instance.

## Steps to Install Jenkins on EC2 Ubuntu Instance

### 1. Launch an EC2 Instance

1. **Log in to AWS Management Console**:
   - Navigate to [AWS Management Console](https://aws.amazon.com/).

2. **Launch Instance**:
   - Go to the EC2 dashboard.
   - Click on "Launch Instance".
   - Select "Ubuntu Server 20.04 LTS (HVM), SSD Volume Type" AMI.
   - Choose an instance type (e.g., t2.micro for free tier).
   - Configure instance details, add storage, add tags, and configure the security group:
     - Allow SSH (port 22)
     - Allow HTTP (port 80)
     - Allow Custom TCP Rule (port 8080)
   - Review and launch the instance, selecting your key pair.

### 2. Connect to Your EC2 Instance

1. **Open Command Prompt or PowerShell**:
   - Navigate to the directory containing your `.pem` file.

2. **Connect to the Instance**:
   ```
   ssh -i "your-key.pem" ubuntu@your-ec2-public-dns


   # Jenkins on AWS EC2

## Overview

Jenkins is an open-source automation server that enables developers to build, test, and deploy their software in a reliable and efficient manner. It is widely used for continuous integration (CI) and continuous delivery (CD) practices. This repository provides a step-by-step guide to installing Jenkins on an Ubuntu EC2 instance on AWS.

## Features of Jenkins

- **Extensible**: With hundreds of plugins in the Update Center, Jenkins integrates with virtually every tool in the CI/CD toolchain.
- **Distributed Builds**: Jenkins can distribute build/test loads to multiple computers.
- **Pipeline**: Provides a way to define a series of steps to be run, either sequentially or in parallel.
- **Easy Installation**: Jenkins can be installed through native system packages, Docker, or even run standalone by any machine with a Java Runtime Environment (JRE) installed.
- **Easy Configuration**: Jenkins is easily set up and configured via its web interface, which includes on-the-fly error checks and built-in help.

## Prerequisites

- **AWS Account**: Ensure you have an active AWS account.
- **EC2 Instance**: An Ubuntu 20.04 LTS EC2 instance.
- **SSH Key**: Your SSH key pair (.pem file) for connecting to the EC2 instance.

## Steps to Install Jenkins on EC2 Ubuntu Instance

### 1. Launch an EC2 Instance

1. **Log in to AWS Management Console**:
   - Navigate to [AWS Management Console](https://aws.amazon.com/).

2. **Launch Instance**:
   - Go to the EC2 dashboard.
   - Click on "Launch Instance".
   - Select "Ubuntu Server 20.04 LTS (HVM), SSD Volume Type" AMI.
   - Choose an instance type (e.g., t2.micro for free tier).
   - Configure instance details, add storage, add tags, and configure the security group:
     - Allow SSH (port 22)
     - Allow HTTP (port 80)
     - Allow Custom TCP Rule (port 8080)
   - Review and launch the instance, selecting your key pair.

### 2. Connect to Your EC2 Instance

1. **Open Command Prompt or PowerShell**:
   - Navigate to the directory containing your `.pem` file.

2. **Connect to the Instance**:
   ```
   ssh -i "your-key.pem" ubuntu@your-ec2-public-dns


    3. Update System Packages


sudo apt-get update
sudo apt-get upgrade -y
4. Install Java


sudo apt-get install openjdk-11-jdk -y
5. Add Jenkins Repository and Key


curl -fsSL https://pkg.jenkins.io/debian/jenkins.io-2023.key | sudo tee /usr/share/keyrings/jenkins-keyring.asc > /dev/null
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] https://pkg.jenkins.io/debian-stable binary/ | sudo tee /etc/apt/sources.list.d/jenkins.list > /dev/null
sudo apt-get update
6. Install Jenkins


sudo apt-get install jenkins -y
7. Start Jenkins Service


sudo systemctl start Jenkins
sudo systemctl enable Jenkins
8. Access Jenkins
Open Port 8080 in Security Group:

Go to EC2 dashboard, select your instance.
Click on the security group, edit inbound rules, add a rule to allow TCP traffic on port 8080.
Open Jenkins in Browser:

Navigate to http://your-ec2-public-dns:8080.
Unlock Jenkins:

Retrieve the initial admin password:


sudo cat /var/lib/jenkins/secrets/initialAdminPassword
Copy the password and paste it into the Jenkins setup wizard.
Complete Jenkins Setup:

Follow the on-screen instructions to complete the setup.
Using Jenkins
Creating a Simple Pipeline
Create a New Job:

Open Jenkins dashboard.
Click on "New Item".
Enter an item name and select "Pipeline".
Configure Pipeline:

Scroll down to the Pipeline section.
Select "Pipeline script" from the Definition dropdown.
Enter your pipeline script.
Example Pipeline Script:

groovy

pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Building...'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing...'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying...'
            }
        }
    }
}
Save and Build:

Click "Save".
Click "Build Now" to run the pipeline.
Troubleshooting
Common Issues
GPG Error: If you encounter a GPG error while adding the Jenkins repository key, ensure you are using the correct key URL and command.
Connection Timeout: Ensure your security group rules are correctly configured to allow necessary traffic.
Service Not Starting: Verify that Java is installed and the Jenkins service is enabled and started.
Resources
Jenkins Official Website
Jenkins Documentation
AWS EC2 Documentation
License
This project is licensed under the MIT License - see the LICENSE file for details.

css


This `README.md` file covers detailed information about Jenkins, including installation steps
, creating a pipeline, troubleshooting, and resources. You can further customize it to match
any additional specifics or preferences you might have.

