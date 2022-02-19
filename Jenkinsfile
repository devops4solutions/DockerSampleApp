pipeline {
    agent any
 stages {
  stage('Docker Build and Tag') {
           steps {
              
                sh 'docker build -t nginxtest:latest .' 
                sh 'docker tag nginxtest saklesh/nginxtest:latest'
                sh 'docker tag nginxtest saklesh/nginxtest:4'
               
          }
        }
     
  stage('Publish image to Docker Hub') {
          
            steps {
        withDockerRegistry([ credentialsId: "saklesh-dockerhub", url: "" ]) {
          sh  'docker push saklesh/nginxtest:latest'
          sh  'docker push saklesh/nginxtest:4' 
        }
                  
          }
        }
     
      stage('Run Docker container on Jenkins Agent') {
             
            steps {
                sh "docker run -d -p 4030:80 saklesh/nginxtest"
 
            }
        }
 stage('Run Docker container on remote hosts') {
             
            steps {
                sh "docker -H ssh://jenkins@172.31.12.143 run -d -p 4001:80 saklesh/nginxtest"
 
            }
        }
    }
}
