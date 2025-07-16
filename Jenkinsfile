pipeline {
  agent any

  stages {
    stage('Checkout') {
      steps {
        cleanWs()
        checkout scm
      }
    }

    stage('Build') {
      agent {
        docker {
          image 'node:18-alpine'
          reuseNode true
        }
      }
      environment {
        NPM_CONFIG_CACHE = '.npm-cache'
      }
      steps {
        sh '''
          ls -la
          rm -rf node_modules
          npm ci
          npm run build
        '''
      }
    }
    stage('Test'){
        steps {
            sh '''
              test -f build/index.html
              npm test
            '''

        }
    }

    stage('Deploy') {
      agent {
        docker {
          image 'node:18-alpine'
          reuseNode true
        }
      }
      steps {
        sh '''
          npm install netlify-cli -g
          netlify --version
        '''
      }
    }
  }

  // post {
  //   always {
  //     junit "test-results/junit.xml"
  //   }
  // }
}
