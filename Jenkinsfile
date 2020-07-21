pipeline {
  agent any
  environment {
    DEPLOY = "${env.BRANCH_NAME == "master" || env.BRANCH_NAME == "develop" ? "true" : "false"}"
    NAME = "xfers-baseimages"
    VERSION = '${BUILD_NUMBER}'
    // REGISTRY = 'xfersprodserver'
    REGISTRY = 'sweetatxfers'
    REGISTRY_CREDENTIAL = 'jenkins-dockerhub'
  }
  stages {
    stage('Build circleci-2.4.4') {
      steps {
        dockerfile {
          filename 'Dockerfile'
          dir 'circleci-2-4-4'
          label '${REGISTRY}/xfers-circleci:2.4.4'
          repositoryUrl 'https://registry.hub.docker.com'
          repositoryCredentialsId '${REGISTRY_CREDENTIAL}'
        }
      }
    }
    stage('Build circleci-2.4.10') {
      steps {
        dockerfile {
          filename 'Dockerfile':w
          dir 'circleci-2-4-10'
          label 'xfersprodserver/xfers-circleci:2.4.10'
          repositoryUrl 'https://registry.hub.docker.com'
          repositoryCredentialsId '${REGISTRY_CREDENTIAL}'
        }
      }
    }
  }
}
