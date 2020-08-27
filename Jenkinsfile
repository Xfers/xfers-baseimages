podTemplate(label: 'mypod', serviceAccount: 'jenkins', containers: [
    containerTemplate(
      name: 'docker',
      image: 'docker',
      command: 'cat',
      ttyEnabled: true
    )
  ],
  volumes: [
    hostPathVolume(mountPath: '/var/run/docker.sock', hostPath: '/var/run/docker.sock'),
  ]
  ) {
    node('mypod') {
        def REPOSITORY_URL = 'https://registry.hub.docker.com'

        def credentials_id = 'dockerhub-credentials'
        def repository_name

        withCredentials([usernamePassword(credentialsId: credentials_id, usernameVariable: 'username')]) {
            repository_name = $username
        }

        stage('Get latest version of code') {
          checkout scm
        }

        stage('Build Image 2-4-4') {
          container('docker') {
            script {
              docker.build("${repository_name}/ruby:2.4.4", "circleci-2-4-4")
            }
          }
        }
        stage('Build Image 2-4-10') {
          container('docker') {
            script {
              docker.build("${repository_name}/ruby:2.4.10", "circleci-2-4-10")
            }
          }
        }
        stage('Push Image 2-4-4') {
          container('docker') {
            script {
              docker.withRegistry(REPOSITORY_URL, "jenkins-dockerhub") {
                docker.image("${repository_name}/ruby:2.4.4").push()
              }
            }
          }
        }
        stage('Push Image 2-4-10') {
          container('docker') {
            script {
              docker.withRegistry(REPOSITORY_URL, "jenkins-dockerhub") {
                docker.image("${repository_name}/ruby:2.4.10").push()
              }
            }
          }
        }
    }
}
