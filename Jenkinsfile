pipeline {
    agent any
 
   tools
    {
       maven 'maven394'
    }
 stages {
      stage('checkout') {
           steps {
             
                git branch: 'master', url: 'https://github.com/kkprbr/jenkins-docker.git'
             
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
                sh 'docker tag samplewebapp 9963565745/samplewebapp:latest'            
          }
        }
     
  stage('Run Docker container on remote hosts') {
             
            steps {
                sh "docker -H ssh://jenkins@10.138.0.4 run -d -p 8080:8080 9963565745/samplewebapp:latest"
 
            }
        }
    }
 }
