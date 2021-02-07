# Jenkins-Hello-World
- [Jenkins-Hello-World](#jenkins-hello-world)
  - [Pre-requisites](#pre-requisites)
  - [Description](#description)
    - [Installing Jenkins](#installing-jenkins)
    - [Start, stop, status](#start-stop-status)
    - [First time login](#first-time-login)
    - [Integrating GitHub with Jenkins](#integrating-github-with-jenkins)
    - [Creating Pipeline](#creating-pipeline)

## Pre-requisites

**You should know** `Docker`, `basic CI-CD concept` & `basics of what Jenkins` is used for

**You should have** `Linux OS` like Ubuntu, `Java` (OpenJDK 11) & `Docker` installed

## Description

This project was created to install Jenkins on a local machine (Ubuntu 16.04) and create a basic pipeline with GitHub & Docker

We will be doing is

* Installing Jenkins and running it, on a local machine
* Creating a docker image
* Pushing it to docker hub using Jenkins' pipeline

___

### Installing Jenkins

1. **Add repository** keystream  
```
wget -q -O - https://pkg.jenkins.io/debian-stable/jenkins.io.key | sudo apt-key add -
```
You must get a response printed as `OK`

2. Now **add the Debian package** to your `sources.list`  
```
sudo sh -c 'echo deb https://pkg.jenkins.io/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list'
```

3. Now, **update system** 
```
sudo apt update
```

4. Finally, **install Jenkins**
```
sudo apt install jenkins
```

Now, **Jenkins is installed** in your system and is ready to run.

### Start, stop, status of Jenkins service

We would be using standard `systemctl` commands

- To start  
```
sudo systemctl start jenkins
```

- To check status  
```
sudo systemctl status jenkins
```

- To stop  
```
sudo systemctl stop jenkins
```

- To start on boot  
```
sudo systemctl enable jenkins
```

### First time login  

1. Go to `<IP_ADDRESS>:8080` 

2. Jenkins login page should appear asking you to enter the administrator password

3. Now open a terminal and type 
```
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

A string printed on the console is the administrator password, enter this is on Jenkins login page  

4. Choose `Install selected plugins` (You may choose `Select plugins to install`)  
Now it will install plugins and show you the details, it takes some time

5. It would ask you to create a new 'Admin User'.

Now, **Jenkins is configured** for the system


### Integrating GitHub with Jenkins

1. Go to `Manage Jenkins` from menu on the left pane

2. Click on `Manage Plugins`

3. Go to `Advance` tab

4. Search & install `GitHub Integration`, `Pipeline`, `Docker` & `Docker Pipeline` plugins

   a. Click on `Download now and install after restart`

   b. On the next window select the checkbox for `Restart Jenkins when installation is complete and no jobs are running` at the bottom of the page. Jenkins will restart once plugin is downloaded

5. Now go to your GitHub repository, go to `Settings`, go to `Webhooks`, click on `Add Webhook`

6. For the payload URL, provide your Jenkins URL and the GitHub webhook path at the end of the URL - `https://<JENKINS_URL>/github-webhook/.`

7. `Content type` should be JSON

8. In `Which events would you like to trigger this webhook?` select `Just the push event.`

Now we are ready to integrate any GitHub repository with Jenkins

### Creating Pipeline

1. On the dashboard, click on `Create Job` option

2. Give name to your pipeline

3. Choose `Pipeline`

4. In `Build Triggers` select `GitHub hook trigger for GITScm polling`

5. In `Pipeline section` choose definition as `Pipeline script from SCM`

6. In the `Source Code Management (SCM)` tab, select `Git` enter GitHub repository URL, and save

7. Now copy [Jenkinsfile](Jenkinsfile) in your repository base path

8. Add Docker credentials to Jenkins host

   a. On the top right of home page, click on dropdown next to the username

   b. Select `Credentials`

   c. Go to `System` OR Click on `Global` from any one pre-existing credentials

   d. Click on `Add Credentials`

   e. Keep scope `Global`

   f. Enter Docker Hub username & password and set some ID in ID field

9. Now in the `Jenkinsfile` in the `environment` set the ID

The pipeline is now created, push code to GitHub to see the pipeline run
