pipeline {
  agent none
  stages {
    stage('Fluffy Build') {
      agent {
        node {
          label 'java8'
        }

      }
      steps {
        sh 'echo Another Placeholder'
        stash(name: 'Java 8', includes: 'target/*')
      }
    }

    stage('Fluffy Test') {
      agent {
        node {
          label 'java8'
        }

      }
      steps {
        sh 'sleep 5'
        sh 'echo Success!'
        unstash 'Java 8'
      }
    }

    stage('Fluffy Deploy') {
      agent {
        node {
          label 'java8'
        }

      }
      steps {
        echo 'Placeholder'
        unstash 'Java 8'
      }
    }

  }
}