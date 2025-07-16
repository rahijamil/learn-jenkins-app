pipeline {
  agent any
  stages {
    stage('Clean Workspace') {
      steps {
        deleteDir()
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
          rm -rf node_modules
          npm ci
          npm run build
        '''
      }
    }
  }
}
