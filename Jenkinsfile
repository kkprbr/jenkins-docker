pipeline {
    agent any
 
   tools
    {
       maven 'maven394'
    }
 stages {
      stage('checkout') {
           steps {
             
                git branch: 'master', url: 'https://github.com/teachmycloud/jenkins-docker.git'
             
          }
        }
  stage('Execute Maven') {
           steps {
             
                sh 'mvn clean compile package'             
          }
        }
stage('Docker Build and Tag') {
           steps {
              
                sh 'docker build -t samplewebapp:latest .' 
                sh 'docker tag samplewebapp teachmycloud/samplewebapp:latest'            
          }
        }
     
  stage('Publish image to Docker Hub') {
          
            steps {
        withDockerRegistry([ credentialsId: "dockerHubcredentials", url: "" ]) {
          sh  'docker push teachmycloud/samplewebapp:latest'
        }
                  
          }
        }
     
      stage('Run Docker container on Jenkins Agent') {
             
            steps 
   {
                sh "docker run -d -p 8003:8080 teachmycloud/samplewebapp"
 
            }
        }
 stage('Run Docker container on remote hosts') {
             
            steps {
                sh "docker -H ssh://jenkins@10.138.0.14 run -d -p 8003:8080 teachmycloud/samplewebapp"
 
            }
        }
    }
 }
