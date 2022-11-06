# Install docker
```sh
sudo hostnamectl set-hostname jenkins-admin
sudo su - ubuntu
sudo apt update -y
sudo apt install docker.io -y
sudo systemctl enable docker.service
sudo systemctl start docker
```
# Install java. Java is a prerequisite for jenkins installation
```sh
sudo apt install openjdk-11-jdk 
java -version
```
# Install Jenkins
```sh
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
```

# Add jenkins user to docker group to be able to run docker commands
```sh
sudo usermod -aG docker jenkins
sudo systemctl enable docker.service
#Add jenkins user to sudoers file to use sudo privileges
sudo echo "jenkins  ALL=(ALL) NOPASSWD:ALL" | sudo tee /etc/sudoers.d/jenkins
sudo su - jenkins
```
 #Install k8s cluster using kops
 ```sh
sudo apt update -y
sudo apt install unzip wget -y
sudo curl https://s3.amazonaws.com/aws-cli/awscli-bundle.zip -o awscli-bundle.zip
sudo apt install unzip python -y
sudo unzip awscli-bundle.zip
sudo ./awscli-bundle/install -i /usr/local/aws -b /usr/local/bin/aws
sudo apt install awscli -y

#Install wget if not installed
sudo apt install wget -y
sudo wget https://github.com/kubernetes/kops/releases/download/v1.22.0/kops-linux-amd64
sudo chmod +x kops-linux-amd64
sudo mv kops-linux-amd64 /usr/local/bin/kops

#Install kubectl
 sudo curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl
 sudo chmod +x ./kubectl
 sudo mv ./kubectl /usr/local/bin/kubectl
 ```
