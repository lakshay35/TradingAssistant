pipeline {
  environment {
    FAILED_STAGE = ""
  }
  agent any

  stages {
    
    stage('Docker Image Build') {
      steps{
        script {
          try {
            docker.build "react-console:latest"
          } catch (e) {
            FAILED_STAGE = "Docker Image Build"
            error "Failed Build"
          }
        }
      }
    }
  }

  post {

    success {
      sendSlackMessage('react-portal', "FAILED ${FAILED_STAGE}: Job: '${env.BUILD_TAG} (${env.BUILD_URL})' on node ${env.NODE_NAME}", '#0d9e0d')
    }

    failure {
      sendSlackMessage('react-portal', "FAILED ${FAILED_STAGE}: Job: '${env.BUILD_TAG} (${env.BUILD_URL})' on node ${env.NODE_NAME}", '#FF0000')
    }
    
    fixed {
      sendSlackMessage('react-portal', "FIXED: Job: '${env.BUILD_TAG}(${env.BUILD_URL})' on node ${env.NODE_NAME}", '##0d9e0d')
    }

    aborted {
      sendSlackMessage('react-portal', "ABORTED: Job: '${env.BUILD_TAG} (${env.BUILD_URL})' on node ${env.NODE_NAME}", '#FFFF00')
    }

    unstable {
      sendSlackMessage('react-portal', "UNSTABLE: Job: '${env.BUILD_TAG} (${env.BUILD_URL})' on node ${env.NODE_NAME}", '#FFFF00')
    }
  } 

}

def sendSlackMessage(String channel, String message, String color) {
  slackSend(channel: channel, message: message, color: color)
}