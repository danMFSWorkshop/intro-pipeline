pipeline {
  agent {
    label 'jdk10'
  }
  stages {
    stage('Say Development') {
      steps {
        echo "Hello ${params.Name}!"
        sh 'java -version'
        echo "${TEST_USER_USR}"
        echo "${TEST_USER_PSW}"
      }
    }
    stage('Testing') {
        parallel {
          stage('Java 8') {
            agent { label 'jdk8a' }
            steps {
              container('jdk8') {
                sh 'java -version'
              }
            }
          }
          stage('Java 10') {
            agent { label 'jdk10' }
            steps {
              container('jdk10') {
                sh 'java -version'
              }
            }
          }
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
    MY_NAME = 'Mary'
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
