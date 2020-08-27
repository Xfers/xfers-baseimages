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
        def ruby_2_4_4
        def ruby_2_4_10

        stage('Get latest version of code') {
          checkout scm
        }

        stage('Build Image 2-4-4') {
          container('docker') {
            withCredentials([usernamePassword(credentialsId: credentials_id, usernameVariable: 'username', passwordVariable: 'password')]) {
              script {
                ruby_2_4_4 = docker.build('$username/ruby:2.4.4', '--net=host circleci-2-4-4')
              }
            }
          }
        }
        stage('Build Image 2-4-10') {
          container('docker') {
            withCredentials([usernamePassword(credentialsId: credentials_id, usernameVariable: 'username', passwordVariable: 'password')]) {
              script {
                ruby_2_4_10 = docker.build('${repository_name}/ruby:2.4.10', '--net=host circleci-2-4-10')
              }
            }
          }
        }
        stage('Push Image 2-4-4') {
          container('docker') {
            script {
              docker.withRegistry(REPOSITORY_URL, "jenkins-dockerhub") {
                ruby_2_4_4.push()
              }
            }
          }
        }
        stage('Push Image 2-4-10') {
          container('docker') {
            script {
              docker.withRegistry(REPOSITORY_URL, "jenkins-dockerhub") {
                ruby_2_4_10.push()
              }
            }
          }
        }
    }
}
