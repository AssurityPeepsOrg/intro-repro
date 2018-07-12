pipeline {
  agent {
    label 'jdk8'
  }
  stages {
    stage('Say hello') {
      steps {
        echo 'hello world'
        sh 'java -version'
      }
    }
  }
  environment {
    MY_NAME = 'Karin'
  }
}