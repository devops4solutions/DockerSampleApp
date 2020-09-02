pipeline {
    agent any
environment 
    {
    dockerhubcredential = credentials('dockerHub')
    registry = "nikhilnidhi/nginxtest"
   }

 stages {
  stage('Docker Build and Tag') {
           steps {
              
                sh 'docker build -t nginxtest:latest .'             
          }
        }
     
  stage('Publish image to Docker Hub') {
          
            steps {
        withDockerRegistry([ credentialsId: "dockerHub", url: "" ]) {
           sh  'docker tag nginxtest nikhilnidhi/nginxtest:latest'
             sh  'docker push nikhilnidhi/nginxtest:latest'         
        }
            
               //sh 'docker login -u ${dockerhubcredential_usr} -p ${dockerhubcredential_psw} nikhilnidhi/nginxtest'
              //sh  'docker tag nginxtest nikhilnidhi/nginxtest:latest'
              //sh  'docker push nikhilnidhi/nginxtest:latest'         
          }
        }
 stage('Run Docker container on remote hosts') {
             
            steps {
                sh "docker -H ssh://jenkins@172.31.28.25 run -d -p 4001:80 nginxtest"
 
            }
        }
    }
}
