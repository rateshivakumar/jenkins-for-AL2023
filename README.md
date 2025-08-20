#!/bin/bash
# =========================================
# Jenkins Installation Script for Amazon Linux 2023
# =========================================

# STEP 1: INSTALL GIT, JAVA, MAVEN
echo "📦 Installing Git, Java 17, Maven..."
sudo yum update -y
sudo yum install -y git maven

# Install Amazon Corretto 17 (Java 17)
sudo amazon-linux-extras enable corretto17
sudo yum install -y java-17-amazon-corretto-devel

# Verify Java
java -version

# STEP 2: ADD JENKINS REPO
echo "📥 Adding Jenkins repo..."
sudo wget -O /etc/yum.repos.d/jenkins.repo https://pkg.jenkins.io/redhat-stable/jenkins.repo
sudo rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io-2023.key

# STEP 3: INSTALL JENKINS
echo "🚀 Installing Jenkins..."
sudo yum install -y jenkins

# STEP 4: CONFIGURE JAVA (Optional if multiple Java versions)
# If multiple Java versions installed, choose Java 17
sudo update-alternatives --config java

# STEP 5: START & ENABLE JENKINS SERVICE
echo "🔧 Starting Jenkins service..."
sudo systemctl start jenkins
sudo systemctl enable jenkins

# STEP 6: CHECK JENKINS STATUS
echo "🔎 Checking Jenkins status..."
sudo systemctl status jenkins

echo "✅ Jenkins installation completed! Access at: http://<YOUR_SERVER_PUBLIC_IP>:8080"
echo "Initial admin password:"
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
