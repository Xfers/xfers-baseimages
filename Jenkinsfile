pipeline {
  agent {
    kubernetes {
      label "jenkins-jenkins-slave default"
    }
  }
  environment {
    REPOSITORY_URL = 'https://registry.hub.docker.com'
    IMAGE_NAME = 'sweetatxfers/xfers-circleci'
    REPO_CRED = 'jenkins-dockerhub'
  }
  stages {
    stage('Get latest version of code') {
      steps {
        checkout scm
      }
    }
    stage('Build Image 2-4-4') {
      steps {
        script {
          docker.build("${IMAGE_NAME}:2.4.4", "circleci-2-4-4")
        }
      }
    }
    stage('Build Image 2-4-10') {
      steps {
        script {
          docker.build("${IMAGE_NAME}:2.4.10", "circleci-2-4-10")
        }
      }
    }
    stage('Push Image 2-4-4'){
      steps {
        script {
          docker.withRegistry("${REPOSITORY_URL}", "jenkins-dockerhub") {
            docker.image("${IMAGE_NAME}:2.4.4").push()
          }
        }
      }
    }
    stage('Push Image 2-4-10'){
      steps {
        script {
          docker.withRegistry("https://registry.hub.docker.com", "jenkins-dockerhub") {
            docker.image("${IMAGE_NAME}:2.4.10").push()
          }
        }
      }
    }
  }
}
