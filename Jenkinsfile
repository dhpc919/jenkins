pipeline {
  agent any
  stages {
    stage('Fluffy Build') {
      steps {
        sh './jenkins/build.sh'
        archiveArtifacts(fingerprint: true, artifacts: 'target/*.jar')
      }
    }

    stage('Fluffy Test') {
      parallel {
        stage('Static') {
          steps {
            sh './jenkins/test-static.sh'
          }
        }

        stage('Backend') {
          steps {
            sh './jenkins/test-backend.sh'
          }
        }

        stage('Frontend') {
          steps {
            sh './jenkins/test-frontend.sh'
          }
        }

        stage('Performance') {
          steps {
            sh './jenkins/test-performance.sh'
          }
        }

      }
    }

    stage('Fluffy Deploy') {
      steps {
        sh './jenkins/deploy.sh staging'
      }
    }

  }
}