pipeline {
  agent any

  stages {
    stage('Build') {
      steps {
        sh 'docker build -t sabarishjoc/web .'
      }
    }
   stage('Deploy') {
      steps {
        withCredentials([usernamePassword(credentialsId: "${DOCKER_REGISTRY_CREDS}", passwordVariable: 'DOCKER_PASSWORD', usernameVariable: 'DOCKER_USERNAME')]) {
          sh "echo \$DOCKER_PASSWORD | docker login -u \$DOCKER_USERNAME --password-stdin docker.io"
          sh 'docker push sabarishjoc/web'
        }
      }
    }
  }
  post {
    always {
      sh 'docker logout'
    }
  }
}
