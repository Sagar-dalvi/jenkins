 a simplified step-by-step guide for setting up Jenkins,
integrating it with GitHub, Maven, and Tomcat, and deploying a Java application.

---

### **Agenda:**

1. **Setup Jenkins**
2. **Setup & Configure Maven and Git**
3. **Setup Tomcat Server**
4. **Integrate GitHub, Maven, and Tomcat with Jenkins**
5. **Create a CI and CD Job**
6. **Test the Deployment**

### **Prerequisites:**

- AWS Account
- Git/GitHub Account with Source Code
- A local machine with CLI Access

### **Step 1: Setup Jenkins Server on AWS EC2 Instance**

1. **Launch an EC2 Instance:**
   - Open EC2 Dashboard in AWS Management Console.
   - Click `Launch Instance`.
   - Choose Amazon Linux 2 AMI (free tier eligible).
   - Select `t2.micro` instance type (free tier eligible).
   - Choose an existing key pair or create a new one.
   - Under Network Settings, select default VPC and enable auto-assign public IP.
   - Create a new Security Group:
     - Allow SSH traffic.
     - Allow TCP port 8080 (Jenkins default port).
   - Click `Launch Instance`.

2. **Connect to Your EC2 Instance:**
   - Copy the SSH command provided in the Connect to instance wizard.
   - Use an SSH client (like MobaXterm) to connect using your `.pem` key.

3. **Install Jenkins:**
   - Update package lists:
     ```bash
     sudo yum update -y
     ```
   - Install Java (required for Jenkins):
     ```bash
     sudo yum install java-11-openjdk-devel -y
     ```
   - Add Jenkins repository and install Jenkins:
     ```bash
     sudo wget -O /etc/yum.repos.d/jenkins.repo https://pkg.jenkins.io/redhat-stable/jenkins.repo
     sudo rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io.key
     sudo yum install jenkins -y
     ```
   - Start Jenkins:
     ```bash
     sudo systemctl start jenkins
     sudo systemctl enable jenkins
     ```
   - Access Jenkins via `http://<your-ec2-public-ip>:8080`.
   - Retrieve the Jenkins admin password:
     ```bash
     sudo cat /var/lib/jenkins/secrets/initialAdminPassword
     ```
   - Log in, install suggested plugins, and create an admin user.

### **Step 2: Integrate GitHub with Jenkins**

1. **Install Git:**
   - Install Git on your EC2 instance:
     ```bash
     sudo yum install git -y
     ```

2. **Install GitHub Plugin:**
   - In Jenkins UI, go to `Manage Jenkins` > `Manage Plugins`.
   - Search for `GitHub Plugin`, install it, and restart Jenkins.

3. **Configure Git:**
   - Go to `Manage Jenkins` > `Global Tool Configuration`.
   - Add Git installation (path auto-detected or provide path manually).

### **Step 3: Integrate Maven with Jenkins**

1. **Install Maven:**
   - Switch to `/opt` directory and download Maven:
     ```bash
     cd /opt
     sudo wget https://dlcdn.apache.org/maven/maven-3/3.9.9/binaries/apache-maven-3.9.9-bin.tar.gz
     sudo tar xzvf apache-maven-3.8.6-bin.tar.gz
     sudo mv apache-maven-3.8.6 maven
     ```

2. **Setup Environment Variables:**
   - Edit `~/.bash_profile` to add Maven and Java paths:
     ```bash
     export JAVA_HOME=/usr/lib/jvm/java-11-openjdk
     export M2_HOME=/opt/maven
     export PATH=$PATH:$M2_HOME/bin
     ```
   - Apply changes:
     ```bash
     source ~/.bash_profile
     ```

3. **Install Maven Plugin:**
   - In Jenkins UI, go to `Manage Jenkins` > `Manage Plugins`.
   - Search for `Maven Integration Plugin`, install it, and restart Jenkins.

4. **Configure Maven and Java:**
   - Go to `Manage Jenkins` > `Global Tool Configuration`.
   - Set JAVA_HOME and Maven locations.

### **Step 4: Setup Tomcat Server**

1. **Launch a New EC2 Instance for Tomcat:**
   - Repeat the EC2 setup steps for a new instance.

2. **Install Java on Tomcat EC2 Instance:**
   - Use the same Java installation commands as before.

3. **Install Tomcat:**
   - Download and install Tomcat:
     ```bash
     cd /opt
     sudo wget https://downloads.apache.org/tomcat/tomcat-9/v9.0.74/bin/apache-tomcat-9.0.74.tar.gz
     sudo tar xzvf apache-tomcat-9.0.74.tar.gz
     sudo mv apache-tomcat-9.0.74 tomcat
     ```
   - Configure Tomcat:
     ```bash
     cd /opt/tomcat
     sudo nano conf/tomcat-users.xml
     ```
     Add user roles and credentials:
     ```xml
     <role rolename="manager-gui"/>
     <role rolename="manager-script"/>
     <user username="admin" password="admin" roles="manager-gui,manager-script"/>
     ```
   - Start Tomcat:
     ```bash
     cd /opt/tomcat/bin
     ./startup.sh
     ```

4. **Access Tomcat Web UI:**
   - Go to `http://<your-tomcat-ec2-public-ip>:8080`.

### **Step 5: Integrate Tomcat with Jenkins**

1. **Install Deploy to Container Plugin:**
   - In Jenkins UI, go to `Manage Jenkins` > `Manage Plugins`.
   - Search for `Deploy to Container Plugin`, install it, and restart Jenkins.

2. **Configure Tomcat Credentials in Jenkins:**
   - Go to `Manage Jenkins` > `Manage Credentials` > `System`.
   - Add new credentials with Tomcat username and password.

### **Step 6: Deploy a Java Application**

1. **Create a New Jenkins Job:**
   - Go to Jenkins Dashboard > `New Item`.
   - Choose `Freestyle Project`, name it, and click `OK`.

2. **Configure Job:**
   - **Source Code Management:**
     - Select `Git` and enter your GitHub repository URL.
   - **Build Steps:**
     - Add a build step to execute Maven goals:
       ```bash
       clean package
       ```
   - **Post-Build Actions:**
     - Add `Deploy war/ear to a container` action.
     - Provide WAR file path, Tomcat URL, and credentials.

3. **Build and Verify:**
   - Click `Build Now` to trigger the build and deployment.
   - Check the Tomcat Manager App to see the deployed application.

4. **Set Up Poll SCM (Optional):**
   - In the Jenkins job configuration, under `Build Triggers`, select `Poll SCM`.
   - Set a schedule for periodic checks (e.g., `* * * * *` for every minute).

### **Conclusion**

You’ve set up Jenkins on AWS EC2, integrated it with GitHub and Maven, 
installed and configured Tomcat, and created a CI/CD pipeline to automate the
 build and deployment of a Java web application. You can now make changes to your 
code and have Jenkins automatically build and deploy updates to Tomcat.

Feel free to adjust any specific settings or configurations based on your environment and project requirements.
