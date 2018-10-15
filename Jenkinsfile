pipeline {
  agent {
    label 'jdk10'
  }
  stages {
    stage('Say Hello') {
      steps {
        echo "Hello ${MY_NAME}!"
        sh 'java -version'
        echo "${TEST_USER_USR}"
        echo "${TEST_USER_PSW}"
      }
    }
  }
  environment {
    MY_NAME = 'Mary'
    TEST_USER = credentials('test-user')
  }
}