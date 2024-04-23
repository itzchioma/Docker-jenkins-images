## Jenkins CI/CD Pipeline for Building and Pushing Docker Images of a Simple Hello World API Implemented in FastAPI to Docker Hub
+ In this tutorial, we will guide you through the process of setting up a Jenkins CI/CD pipeline to automate the building and pushing of Docker images to Docker Hub. We will use a simple FastAPI “Hello World” application as our example code.

#### Requirements
+  Jenkins Installed on EC2: Jenkins should be installed and running on your EC2 instance. You can access Jenkins through the web interface.

#### Setup Ec2 instance
+  Go to the AWS console and search for the EC2 instance (Ubuntu)
![Launching-an-instance](https://github.com/itzchioma/Docker-jenkins-images/blob/main/asset/Launching-an-instance.png)
+  Ssh into the Instance you created
![ssh-instance](https://github.com/itzchioma/Docker-jenkins-images/blob/main/asset/ssh-instance.png)
  

<!-- Updating the ubuntu server (Prepping the server for configuration) -->

```bash
sudo apt update
sudo apt install fontconfig openjdk-17-jre
java -version
```
<!--Now, you need to execute the following commands to install Jenkins -->
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

 + In the AWS console, edit the inbound rules for the security group and add the rules as depicted in the image below.
![Port8080](https://github.com/itzchioma/Docker-jenkins-images/blob/main/asset/Port8080.png)

 + After setting up the server, you can access your application by entering the IP address followed by the port number,like this:http://your_ip_address:8080 you will find this window
![Welcome-jenkins](https://github.com/itzchioma/Docker-jenkins-images/blob/main/asset/Welcome-jenkins.png)

 + in consloe you past this like as show below
![Welcome-jenkins](https://github.com/itzchioma/Docker-jenkins-images/blob/main/asset/Welcome-jenkins.png)

 + after will redirect this page
![Jenkins-admin-profile](https://github.com/itzchioma/Docker-jenkins-images/blob/main/asset/Jenkins-admin-profile.png)

 + Now, to successfully access the Jenkins homepage
![Jenkins-start-up](https://github.com/itzchioma/Docker-jenkins-images/blob/main/asset/Jenkins-start-up.png)

 + Docker Installed on Jenkins Server:Ensure that Docker is installed on the Jenkins server. You can use the official Docker installation instructions for your Linux distribution.

 ```bash
sudo apt update
sudo apt install -y apt-transport-https ca-certificates curl software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
echo "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt update
sudo apt install -y docker-ce docker-ce-cli containerd.io 
```

+ Docker Hub Account:Create an account on Docker Hub if you don’t have one. Visit the Docker Hub Website: Open your web browser and go to the Docker Hub website: https://hub.docker.com/ Click on “Sign Up”: Locate the “Sign Up” button on the top right corner of the page and click on it. Fill in Registration Details:Enter a valid email address.Choose a username for your Docker Hub account.Create a strong password. Create repo with test.

+ Dockerfile in Your GitHub Repository:Your GitHub repository should contain a Dockerfile in the root directory. This Dockerfile defines the instructions for building your Docker image.

+ This is my repository; you can check it https://github.com/itzchioma/Docker-jenkins-images

+ Here, I am building a Docker image for FastAPI this my Dockerfile

+ Jenkins Pipeline Configuration:Configure a Jenkins pipeline with the provided Jenkinsfile. Adjust the placeholders in the Jenkinsfile, such as repository URL, Docker Hub credentials, etc.
+ Webhook or Polling Setup: Set up a webhook in your GitHub repository to trigger the Jenkins pipeline on code changes. Alternatively, you can configure Jenkins to poll your repository for changes.
+ Payload URL: publicIP with port and in trigger in webhook select pull request, pushes.
![configure-jenkins-webhook](https://github.com/itzchioma/Docker-jenkins-images/blob/main/asset/configure-jenkins-webhook.png)

+ Docker Hub Credentials in Jenkins:In Jenkins, set up Docker Hub credentials. Go to “Jenkins” > “Manage Jenkins” > “Manage Credentials” > “(select your domain)” > “(select your credentials)”.
![Docker-credential-setup](https://github.com/itzchioma/Docker-jenkins-images/blob/main/asset/Docker-credential-setup.png)

+ Now, you’ve added Docker Hub credentials to Jenkins. with username and password.
![docker-hub-credentials](https://github.com/itzchioma/Docker-jenkins-images/blob/main/asset/docker-hub-credentials.png)

+ Jenkins Plugins:Ensure that the necessary Jenkins plugins are installed. You may need plugins related to Docker integration and pipeline execution. Install them via the Jenkins web interface under “Manage Jenkins” > “Manage Plugins.”
![docker-installed-plugins](https://github.com/itzchioma/Docker-jenkins-images/blob/main/asset/docker-installed-plugins.png)
+ I already installed all plugins you check here.
+ In Manage Jenkins you can add JDK installations and Git installations , Docker installations

## Note:
+ Internet Access from Jenkins Server:Ensure that the Jenkins server has internet access to pull Docker images and push to Docker Hub.
+ GitHub Integration:Jenkins should be able to access your GitHub repository. If it's a private repository, make sure to set up the necessary credentials or SSH keys.
+ EC2 Security Group Configuration:Ensure that the security group associated with your EC2 instance allows traffic on the necessary ports for Jenkins and Docker.

## Jenkins Dashboard
+ In Dashboard page Now, click on the ‘New Item’ option located at the top left
![Jenkins-start-up](https://github.com/itzchioma/Docker-jenkins-images/blob/main/asset/Jenkins-start-up.png)
+ Click on ‘Give Item Name,’ select ‘Pipeline,’ and click ‘OK
+ In the description, add your description, and in Build Triggers, select ‘GitHub hook trigger for GITScm polling.
+ In the pipeline section, choose ‘Pipeline script from SCM,’ and under SCM, add the Git Repository URL. Specify your Branch Specifier as blank for ‘any. apply it and save.
+ Build will be triggered automatically as shown in the image below.

