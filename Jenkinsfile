podTemplate(label: 'mypod', serviceAccount: 'jenkins-ci', containers: [
    containerTemplate(
      name: 'docker',
      image: 'docker',
      command: 'cat',
      resourceRequestCpu: '100m',
      resourceLimitCpu: '300m',
      resourceRequestMemory: '300Mi',
      resourceLimitMemory: '500Mi',
      ttyEnabled: true
    )
  ],
  volumes: [
    hostPathVolume(mountPath: '/var/run/docker.sock', hostPath: '/var/run/docker.sock'),
  ]
  ) {
    node('mypod') {
        def REPOSITORY_URL = 'https://registry.hub.docker.com'
        def IMAGE_NAME = 'sweetatxfers/xfers-circleci'
        def REPO_CRED = 'jenkins-dockerhub'

        stage('Get latest version of code') {
          checkout scm
        }
        stage('Build Image 2-4-4') {
          container('docker') {
            script {
              docker.build("sweetatxfers/xfers-circleci:2.4.4", "circleci-2-4-4")
            }
          }
        }
        stage('Build Image 2-4-10') {
          container('docker') {
            script {
              docker.build("sweetatxfers/xfers-circleci:2.4.10", "circleci-2-4-10")
            }
          }
        }
        stage('Push Image 2-4-4'){
          container('docker') {
            script {
              docker.withRegistry("${REPOSITORY_URL}", "jenkins-dockerhub") {
                docker.image("sweetatxfers/xfers-circleci:2.4.4").push()
              }
            }
          }
        }
        stage('Push Image 2-4-10'){
          container('docker') {
            script {
              docker.withRegistry("https://registry.hub.docker.com", "jenkins-dockerhub") {
                docker.image("sweetatxfers/xfers-circleci:2.4.10").push()
              }
            }
          }
        }
    }
}
