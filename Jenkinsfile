pipeline {
  agent {
    label 'jdk8'
  }
  stages {
     stage('Testing') {
        parallel {
          stage('Java 8') {
            agent { label 'jdk9' }
            steps {
              container('maven8') {
                sh 'mvn -v'
              }
            }
          }
          stage('Java 9') {
            agent { label 'jdk8' }
            steps {
              container('maven9') {
                sh 'mvn -v'
              }
            }
          }
        }
     }
        stage('Checkpoint') {
          steps {
            checkpoint 'Checkpoint'
          }
        }
        stage('Java 9') {
          agent {
            label 'jdk9'
          }
          steps {
            sh 'java -version'
            sleep(time: 20, unit: 'SECONDS')
          }
        }
    stage('Deploy') {
      options {
        timeout(time: 30, unit: 'SECONDS')
      }
      input {
        message 'Which Version?'
        id 'Deploy'
        parameters {
          choice(name: 'APP_VERSION', choices: '''v1.1
v1.2
v1.3''', description: 'What to deploy?')
        }
      }
      steps {
        echo "Deploying ${APP_VERSION}."
      }
    }
    stage('Get Kernel') {
      steps {
        script {
          try {
            KERNEL_VERSION = sh (script: "uname -r", returnStdout: true)
          } catch(err) {
            echo "CAUGHT ERROR: ${err}"
            throw err
          }
        }

      }
    }
    stage('Say Kernel') {
      steps {
        echo "${KERNEL_VERSION}"
      }
    }
  }
  environment {
    MY_NAME = 'Karin'
    TEST_USER = credentials('test-user')
  }
  post {
    aborted {
      echo 'Why didn\'t you push my button?'

    }

  }
  parameters {
    string(name: 'Name', defaultValue: 'whoever you are', description: 'Who should I say hi to?')
  }
}
