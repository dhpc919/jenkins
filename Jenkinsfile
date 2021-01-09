pipeline {
  agent {
    node {
      label 'java7'
    }

  }
  stages {
    stage('Fluffy Build') {
      steps {
        sh 'echo Another Placeholder'
      }
    }

    stage('Fluffy Test') {
      steps {
        sh 'sleep 5'
        sh 'echo Success!'
      }
    }

    stage('Fluffy Deploy') {
      steps {
        echo 'Placeholder'
      }
    }

  }
}