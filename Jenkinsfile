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
      steps {
        sh './jenkins/test-all.sh'
        junit(testResults: 'target/**/TEST*.xml', allowEmptyResults: true)
      }
    }

    stage('Fluffy Deploy') {
      steps {
        sh './jenkins/deploy.sh staging'
      }
    }

  }
}