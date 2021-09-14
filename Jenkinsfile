pipeline {
  environment {
    BRANCH_NAME="main"
    Jenkinsfile_repo_git = "https://github.com/Assistantit/testJavaAppCICD"
    Project_repo_git = "https://github.com/Assistantit/testJavaAppCICD"
    registry = "griml/javahillelwebapp"
    registryCredential = 'dockerhub'
    dockerImage = ''
  }
  agent any
  stages {
    stage('Cloning Git') {
      steps {
        //Cloning repo project
        git credentialsId: 'github_connection', url: "${Project_repo_git}", branch: "${BRANCH_NAME}" 
        
      }
    }
    stage('Building image') {
      steps{
        script {
          dockerImage = docker.build (registry + ":$BUILD_NUMBER", "-f ./docker/Dockerfile ./docker")
        }
      }
    }
    stage('Deploy Image') {
      steps{
        script {
          docker.withRegistry( '', registryCredential ) {
            dockerImage.push()
          }
        }
      }
    }
    stage('Remove Unused docker image') {
      steps{
        sh "docker rmi $registry:$BUILD_NUMBER"
      }
    }
  }
}
