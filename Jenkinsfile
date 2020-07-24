pipeline {
  agent { docker }
  stages {
    def REPOSITORY_URL = 'https://registry.hub.docker.com'
    def IMAGE_NAME = 'sweetatxfers/xfers-circleci'
    def REPO_CRED = 'jenkins-dockerhub'

    stage('Get latest version of code') {
      checkout scm
    }
    stage('Build Image 2-4-4') {
      script {
        docker.build("sweetatxfers/xfers-circleci:2.4.4", "circleci-2-4-4")
      }
    }
    stage('Build Image 2-4-10') {
      script {
        docker.build("sweetatxfers/xfers-circleci:2.4.10", "circleci-2-4-10")
      }
    }
    stage('Push Image 2-4-4'){
      script {
        docker.withRegistry("${REPOSITORY_URL}", "jenkins-dockerhub") {
          docker.image("sweetatxfers/xfers-circleci:2.4.4").push()
        }
      }
    }
    stage('Push Image 2-4-10'){
      script {
        docker.withRegistry("https://registry.hub.docker.com", "jenkins-dockerhub") {
          docker.image("sweetatxfers/xfers-circleci:2.4.10").push()
        }
      }
    }
  }
}
