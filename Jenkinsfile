pipeline {
  agent {
    docker {
      args '-p 3000:3000'
      image 'node:lts-alpine'
    }

  }
  stages {
    stage('build') {
      steps {
        sh 'npm install'
      }
    }

    stage('test') {
      environment {
        CI = 'true'
      }
      steps {
        sh './jenkins/scripts/test.sh'
      }
    }

    stage('deliver') {
      steps {
        sh './jenkins/scripts/deliver.sh'
        input 'finished using the web site?(click "proceed" to continue)'
        sh './jenkins/scripts/kill.sh'
      }
    }

  }
}