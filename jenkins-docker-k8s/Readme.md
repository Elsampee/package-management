---sh
# Install docker
sudo hostnamectl set-hostname jenkins-admin
sudo su - ubuntu
sudo apt update -y
sudo apt install docker.io -y
sudo systemctl enable docker.service
sudo systemctl start docker
---

---sh
# Install jenkins
sudo apt install openjdk-11-jdk #Java is a prerequisite for jenkins installation
java -version
# Install Jenkins
curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io.key | sudo tee \
  /usr/share/keyrings/jenkins-keyring.asc > /dev/null
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
  https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null
sudo apt-get update
sudo apt-get install jenkins
# Start Jenkins
sudo systemctl daemon-reload  # To Register the Jenkins service 
sudo systemctl start jenkins
systemctl status jenkins
---

# Add jenkins user to docker group to be able to run docker commands
---sh
sudo usermod -aG docker jenkins
sudo systemctl enable docker.service
#Add jenkins user to sudoers file to use sudo privileges
sudo echo "jenkins  ALL=(ALL) NOPASSWD:ALL" | sudo tee /etc/sudoers.d/jenkins
sudo su - jenkins
---
 
