# Connect to your EC2 instance
ssh -i "your-key.pem" ubuntu@your-ec2-public-dns

# Update and upgrade system packages
sudo apt-get update
sudo apt-get upgrade -y

# Install Java
sudo apt-get install openjdk-11-jdk -y

# Add Jenkins repository key
curl -fsSL https://pkg.jenkins.io/debian/jenkins.io-2023.key | sudo tee /usr/share/keyrings/jenkins-keyring.asc > /dev/null

# Add Jenkins repository
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] https://pkg.jenkins.io/debian-stable binary/ | sudo tee /etc/apt/sources.list.d/jenkins.list > /dev/null

# Update package list again
sudo apt-get update

# Install Jenkins
sudo apt-get install jenkins -y

# Start and enable Jenkins
sudo systemctl start jenkins
sudo systemctl enable jenkins

# Retrieve initial admin password


sudo cat /var/lib/jenkins/secrets/initialAdminPassword

   #in jenkins
inter the Jenkins to create user name and password and next step following,
of plugging selection and start the jenkins
