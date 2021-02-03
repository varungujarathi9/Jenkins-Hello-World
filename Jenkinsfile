properties([pipelineTriggers([githubPush()])])

pipeline {
    environment {
        // name of the image without tag
        dockerRepo = "varungujarathi9/jenkins-hello-world"
        dockerCredentials = 'docker_hub'
        dockerImage = ""
    }

    agent any

    stages {
        /* checkout repo */
        stage('Checkout SCM') {
            steps {
                checkout([
                 $class: 'GitSCM',
                 branches: [[name: 'master']],
                 userRemoteConfigs: [[
                    url: 'https://www.github.com/varungujarathi9/Jenkins-Hello-World.git',
                    credentialsId: '',
                 ]]
                ])
            }
        }
        stage("Building docker image"){
            steps{
                script{
                    dockerImage = docker.build dockerRepo + ":$BUILD_NUMBER"
                }
            }
        }
        stage("Pushing image to registry"){
            steps{
                script{
                    // if you want to use custom registry, use the first argument, which is blank in this case
                    docker.withRegistry( '', dockerCredentials){
                        dockerImage.push()
                    }
                }
            }
        }
        stage('Cleaning up') {
            steps {
                sh "docker rmi $registry:$BUILD_NUMBER"
            }
        }
    }

    /* Cleanup workspace */
    post {
       always {
           deleteDir()
       }
   }
}