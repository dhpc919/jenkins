pipeline {
  agent none
  stages {
    stage ("start") {

      steps {
        withCredentials([
            usernamePassword(
                credentialsId: 'stupid-id', 
                usernameVariable: 'USER', 
                passwordVariable: 'PASS'
                )]) {
            sh '''
                echo "The username is: ${USER}"
                echo "The password is : ${PASS}"
            '''
        }
      }
    }
    stage('Fluffy Build') {
      parallel {
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

    stage('Confirm Deploy') {
      steps {
        input(message: 'You are prompted to confirm the deployment', ok: 'Confirm', submitter: 'derrick')
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
        sh './jenkins/deploy.sh staging'
      }
    }



  }
}