pipeline {
  agent { label 'linux' }
  options {
    buildDiscarder(logRotator(numToKeepStr: '5'))
  }
  environment {
    DOCKERHUB_CREDENTIALS = credentials('rajat9893308210')
  }
  stages {
    stage('Build') {
      steps {
        sh 'docker build -t rajat9893308210/dp-alpine:latest .'
      }
    }
    stage('Login') {
      steps {
        sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
      }
    }
    stage('Push') {
      steps {
        sh 'docker push rajat9893308210/dp-alpine:latest'
      }
    }
  }
  post {
    always {
      sh 'docker logout'
    }
  }
}
