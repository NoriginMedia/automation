// TODO
// https://github.com/cypress-io/cypress-example-kitchensink/blob/master/Jenkinsfile
pipeline {
  agent {label 'slave-dc01'}
  tools {nodejs "node"}
  stages {
    stage('Preflight') {
      steps {
        echo "====++++Preflight++++===="
        sh 'node -v'
        sh 'npm --version'
        sh 'rm -rf node_modules'
        sh 'npm install'
      }
    }
    stage('Test') {
      steps {
        sh 'npm run test:ui'
      }      
    }
    stage('After test'){
      steps {
        echo "====++++After test++++===="
      }
    }
  }
  post {
    success {
       echo "====++++success++++===="
    }
    failure {
      echo "====++++failure++++===="
    }  
  }
}
