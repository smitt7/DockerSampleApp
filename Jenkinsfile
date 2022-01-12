pipeline {
    agent any
 stages {
  stage('Docker Build and Tag') {
           steps {
              
                sh 'docker build -t nginxtest:latest .' 
                sh 'docker tag nginxtest smatty7/nginxtest:latest'
                sh 'docker tag nginxtest smatty7/nginxtest:$BUILD_NUMBER'
               
          }
        }
     
  stage('Publish image to Docker Hub') {
          
            steps {
        withDockerRegistry([ credentialsId: "dockerHub", url: "" ]) {
          sh  'docker push smatty7/nginxtest:latest'
          sh  'docker push smatty7/nginxtest:$BUILD_NUMBER' 
        }
                  
          }
        }
     
   stage('Run Docker container on remote hosts') {
             
            steps {
                sh "docker -H ssh://ec2-user@3.93.153.243 run -d -p 4001:80 smatty7/nginxtest"
 
            }
        }
    }
}
