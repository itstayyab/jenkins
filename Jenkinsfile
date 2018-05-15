pipeline {
  agent any
  stages {
    stage('Prep') {
      parallel {
        stage('Prep') {
          steps {
            echo 'This is a prep task'
            sh 'ls -ltr'
            input(message: 'Enter value', id: '1', ok: 'start', submitterParameter: 'Dev,SQE,PPR,PROD')
          }
        }
        stage('prep based down') {
          steps {
            sleep 2
          }
        }
        stage('error') {
          steps {
            writeFile(file: 'test.txt', text: 'Tada', encoding: 'utf8')
            echo '${env.name}'
          }
        }
      }
    }
    stage('Evaluate') {
      parallel {
        stage('Evaluate') {
          steps {
            sh 'cat test.txt'
          }
        }
        stage('eval based down') {
          steps {
            sh 'echo "more content in txt file" >> test.txt'
          }
        }
        stage('print message') {
          steps {
            sh 'cat test.txt'
          }
        }
      }
    }
    stage('Last Stage') {
      parallel {
        stage('Last Stage') {
          steps {
            sh 'cat test.txt'
          }
        }
        stage('error') {
          steps {
            sh 'echo "last stage" >> test.txt'
          }
        }
        stage('finished') {
          steps {
            sh 'cp test.txt test_1.txt '
            sh 'rm -f test.txt'
          }
        }
      }
    }
    stage('bye') {
      steps {
        echo 'finsihed'
        echo 'This is ${env.env}'
      }
    }
  }
  environment {
    env = 'Dev'
    name = 'tayyab'
  }
}