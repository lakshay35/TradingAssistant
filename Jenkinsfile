pipeline {

  environment {
    registry = "908173109448.dkr.ecr.us-east-2.amazonaws.com/personal"
    registryCredential = 'ECR'
  }

  agent any
  stages {
    stage('Building image') {
      steps{
        script {
          docker.build registry + ":$BUILD_NUMBER"
        }
      }
    }
  }
}