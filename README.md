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

You should know Docker, basic CI-CD concept & basics of what Jenkins is used for

You should have Linux(Debian) OS like Ubuntu, Java (openJDK) & Docker CE installed

## Description  

This project was created to install Jenkins on local machine (Ubuntu 16.04) and create a basic pipeline with GitHub

We will be

- Installing Jenkins and running it, on local machine
- Creating a docker image
- Pushing it to docker hub using Jenkins' pipeline

___

### Installing Jenkins

1. Add repository key stream  
   `wget -q -O - https://pkg.jenkins.io/debian-stable/jenkins.io.key | sudo apt-key add -`  
   You must get an repose printed as `OK`

2. Now add the Debian package to your `sources.list`  
    `sudo sh -c 'echo deb https://pkg.jenkins.io/debian-stable binary/ > \
    /etc/apt/sources.list.d/jenkins.list'`

3. Now, `update` system  
   `sudo apt update`

4. Finally, install Jenkins  
   `sudo apt install jenkins`

Now, Jenkins is installed in your system and is ready to run.

### Start, stop, status

We would be using standard `systemctl` commands

1. To start  
   `sudo systemctl start jenkins`

2. To check status  
   `sudo systemctl status jenkins`

3. To stop  
   `sudo systemctl stop jenkins`

4. To start on boot  
   `sudo systemctl enable jenkins`

### First time login  

1. Go to `localhost:8080`

2. Jenkins login page should appear asking you to enter the administrator password

3. Now open a terminal and type `sudo cat /var/lib/jenkins/secrets/initialAdminPassword`  
The string printed on console is the administrator password, enter this is on Jenkins login page  

4. Choose `Install selected plugins` (You may choose `Select plugins to install`)  
Now it will install plugins and show you the details, it takes some time

5. It would ask you to create a new 'Admin User'.

Now, Jenkins is installed and configured for system

### Integrating GitHub with Jenkins

1. Go to `Manage Jenkins` from menu on the left pane

2. Click on `Manage Plugins`

3. Go to `Advance` tab

4. Search & install `GitHub Integration` plugin

   a. Click on `Download now and install after restart`

   b. On the next window select the checkbox for `Restart Jenkins when installation is complete and no jobs are running` at the bottom of the page. Jenkins will restart once plugin is downloaded

5. Now, go to `Configure System` in `Manage Jenkins`

6. Scroll down to `Git plugin`
   a. Add your GitHub username & email address

Now we are ready to integrate any GitHub repository with Jenkins

### Creating Pipeline

1. On the dashboard, click on `Create Job` option

2. Give name to your pipeline

3. Choose `Freestyle project`

4. In the `Source Code Management` tab 