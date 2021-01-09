pipeline {
  agent none
  stages {
    stage('Fluffy Build') {
      parallel {
        stage('Fluffy Build') {
          agent {
            node {
              label 'java8'
            }

          }
          steps {
            sh 'echo Another Placeholder'
            stash(name: 'Java 8', includes: 'target/')
          }
        }

        stage('Build Java 7') {
          agent {
            node {
              label 'java7'
            }

          }
          steps {
            stash(name: 'java 7', includes: 'target/java 7/*')
            archiveArtifacts(artifacts: 'target/java 7/text.txt', fingerprint: true)
          }
        }

        stage('Build Java 8') {
          agent {
            node {
              label 'java8'
            }

          }
          steps {
            stash(name: 'java 8', includes: 'target/java 8/*')
          }
        }

      }
    }

    stage('Fluffy Test') {
      parallel {
        stage('Fluffy Test') {
          agent {
            node {
              label 'java8'
            }

          }
          steps {
            sh 'sleep 5'
            sh 'echo Success!'
          }
        }

        stage('Java 7 Test 1') {
          agent {
            node {
              label 'java7'
            }

          }
          steps {
            unstash 'java 7'
          }
        }

        stage('Java 7 Test 2') {
          agent {
            node {
              label 'java7'
            }

          }
          steps {
            unstash 'java 7'
          }
        }

        stage('Java 8 Test 1') {
          agent {
            node {
              label 'java8'
            }

          }
          steps {
            unstash 'java 8'
          }
        }

        stage('Java 8 Test 2') {
          agent {
            node {
              label 'java8'
            }

          }
          steps {
            unstash 'java 8'
          }
        }

      }
    }

    stage('Fluffy Deploy') {
      agent {
        node {
          label 'java7'
        }

      }
      steps {
        echo 'Placeholder'
        unstash 'java 7'
      }
    }

  }
}