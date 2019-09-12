pipeline {
  agent {label 'slave-dc01'}
  tools {nodejs "node"}
  stages {
    stage('Preflight') {
      steps {
        echo "====++++Preflight++++===="
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
