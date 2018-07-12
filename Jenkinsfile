pipeline {
  agent any
  stages {
    stage('Say hello') {
      agent {
        node {
          label 'jdk9'
        }

      }
      steps {
        echo 'hello world'
        sh 'java -version'
      }
    }
  }
}