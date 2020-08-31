pipeline {
    agent any
environment 
    {
    dockerHub = 'dockerhub'
   }
 stages {
      stage('checkout') {
           steps {
             
                git branch: 'master', url: 'https://github.com/devops4solutions/CI-CD-using-Docker.git'
             
          }
        }
  stage('Docker Build and Tag') {
           steps {
             
                sh 'docker build -t nginxtest:latest .'             
          }
        }
     
  stage('Publish image to Docker Hub') {
           steps {
             
               sh 'docker login -u {dockerHub_usr} -p {dockerhub_psw}'
              sh  'docker tag nginxtest nikhilnidhi/nginxtest:latest'
              sh  'docker push nikhilnidhi/nginxtest:latest'         
          }
        }
 stage('Run Docker container on remote hosts') {
             
            steps {
                sh "docker -H ssh://jenkins@172.31.28.25 run -d -p 4001:80 nginxtest"
 
            }
        }
    }
}
