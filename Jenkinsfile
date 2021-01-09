pipeline {
  agent any
  stages {
    stage('start') {
      steps {
        withCredentials(bindings: [
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
              post {
                success {
                  stash(name: 'java 7', includes: 'target/java 7/*')
                  archiveArtifacts(artifacts: 'target/java 7/text.txt', fingerprint: true)
                }

              }
              steps {
                echo 'sth'
              }
            }

            stage('Build Java 8') {
              agent {
                node {
                  label 'java8'
                }

              }
              post {
                success {
                  stash(name: 'java 8', includes: 'target/java 8/*')
                }

              }
              steps {
                echo 'sth'
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
                sh 'sleep 1'
                sh 'echo Success!'
              }
            }

            stage('Java 7 Test 1') {
              agent {
                node {
                  label 'java7'
                }

              }
              post {
                success {
                  unstash 'java 7'
                }

              }
              steps {
                echo 'sth'
              }
            }

            stage('Java 7 Test 2') {
              agent {
                node {
                  label 'java7'
                }

              }
              post {
                success {
                  unstash 'java 7'
                }

              }
              steps {
                echo 'sth'
              }
            }

            stage('Java 8 Test 1') {
              agent {
                node {
                  label 'java8'
                }

              }
              post {
                success {
                  unstash 'java 8'
                }

              }
              steps {
                echo 'sth'
              }
            }

            stage('Java 8 Test 2') {
              agent {
                node {
                  label 'java8'
                }

              }
              post {
                success {
                  unstash 'java 8'
                }

              }
              steps {
                echo 'sth'
              }
            }

          }
        }

        stage('Confirm Deploy') {
          when {
            branch 'main'
          }
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
          when {
            branch 'main'
          }
          steps {
            echo 'Placeholder'
            unstash 'java 7'
            sh './jenkins/deploy.sh staging'
          }
        }

      }
    }