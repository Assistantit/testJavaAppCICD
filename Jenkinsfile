pipeline {
  environment {
    BRANCH_NAME="develop"
    Jenkinsfile_repo_git = "https://github.com/your_repo.git"
    Project_repo_git = "https://github.com/your_repo_image.git"
    registry = "devops/docker-test"
    registryCredential = 'dockerhubCredTEST'
    dockerImage = ''
  }
  agent any
  stages {
    stage('Cloning Git') {
      steps {
        //Cloning repo project
        git credentialsId: 'gitHubCred', url: "${Project_repo_git}", branch: "${BRANCH_NAME}" 
        sh 'ls -la /var/jenkins_home/workspace/'
        
      }
    }
    stage('Building image') {
      steps{
        script {
          dockerImage = docker.build (registry + ":$BUILD_NUMBER", "-f ./Docker/Dockerfile ./Docker")
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
