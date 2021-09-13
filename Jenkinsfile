pipeline {
    agent any
	
	  tools
    {
       maven "Maven"
    }
 stages {
      stage('checkout') {
           steps {
             
                git branch: 'main', url: 'https://github.com/Assistantit/testJavaAppCICD.git'
             
          }
        }
	 stage('Execute Maven') {
           steps {
             
                sh 'mvn package'             
          }
        }
        

     stage('Docker Build and Tag') {
           steps {
              
                sh 'docker build -t javahillelwebapp:latest .' 
                sh 'docker tag JavaHillelwebapp griml/javahillelwebapp:latest'
                //sh 'docker tag samplewebapp griml/javahillelwebapp:$BUILD_NUMBER'
               
                 }
        }
     
     stage('Publish image to Docker Hub') {
          
            steps {
                  withDockerRegistry([ credentialsId: "dockerHub", url: "" ]) {
                  sh  'docker push griml/javahillelwebapp:latest'
                  //sh 'docker tag samplewebapp griml/JavaHillelwebapp:$BUILD_NUMBER' 
                }
                  
            }
        }
     
#     stage('Run Docker container on Jenkins Agent') {
#             
#            steps {
#                sh "docker run -d -p 8003:8080 griml/javahillelwebapp"
#                }
#        }
#     stage('Run Docker container on remote hosts') {
#             
#            steps {
#                sh "docker -H ssh://jenkins@172.31.28.25 run -d -p 8003:8080 griml/javahillelwebapp"
# 
#            }
#       }
    }
}