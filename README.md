## Jenkins CI/CD Pipeline for Building and Pushing Docker Images of a Simple Hello World API Implemented in FastAPI to Docker Hub
###  In this tutorial, we will guide you through the process of setting up a Jenkins CI/CD pipeline to automate the building and pushing of Docker images to Docker Hub. We will use a simple FastAPI “Hello World” application as our example code.

#### Requirements
+  Jenkins Installed on EC2: Jenkins should be installed and running on your EC2 instance. You can access Jenkins through the web interface.

#### Setup Ec2 instance
+  Go to the AWS console and search for the EC2 instance (Ubuntu)
+  Ssh into the Instance you created
  

<!-- Updating the ubuntu server (Prepping the server for configuration) -->

```bash
sudo apt update
sudo apt install fontconfig openjdk-17-jre
java -version
```
<1--Now, you need to execute the following commands to install Jenkins -->
<!-- Installing Jenkins via command line -->
```bash
sudo wget -O /usr/share/keyrings/jenkins-keyring.asc \
  https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
  https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null
sudo apt-get update
sudo apt-get install jenkins
```

<!-- To start the jenkins you need to perfrom this command -->
```bash
 sudo systemctl enable jenkins
 sudo systemctl start jenkins
 sudo systemctl status jenkins
 ```

 ### In the AWS console, edit the inbound rules for the security group and add the rules as depicted in the image below.

 ### After setting up the server, you can access your application by entering the IP address followed by the port number,like this:http://your_ip_address:8080 you will find this window

 ### in consloe you past this like as show below

 ### after will redirect this page

 ### Now, to successfully access the Jenkins homepage

 ### Docker Installed on Jenkins Server:Ensure that Docker is installed on the Jenkins server. You can use the official Docker installation instructions for your Linux distribution.

 ```bash
sudo apt update
sudo apt install -y apt-transport-https ca-certificates curl software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
echo "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt update
sudo apt install -y docker-ce docker-ce-cli containerd.io 
```

### Docker Hub Account:Create an account on Docker Hub if you don’t have one. Visit the Docker Hub Website: Open your web browser and go to the Docker Hub website: https://hub.docker.com/ Click on “Sign Up”: Locate the “Sign Up” button on the top right corner of the page and click on it. Fill in Registration Details:Enter a valid email address.Choose a username for your Docker Hub account.Create a strong password. Create repo with test.

### Dockerfile in Your GitHub Repository:Your GitHub repository should contain a Dockerfile in the root directory. This Dockerfile defines the instructions for building your Docker image.

### This is my repository; you can check it 

### Here, I am building a Docker image for FastAPI this my Dockerfile

### Jenkins Pipeline Configuration:Configure a Jenkins pipeline with the provided Jenkinsfile. Adjust the placeholders in the Jenkinsfile, such as repository URL, Docker Hub credentials, etc.