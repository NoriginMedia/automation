// Utility functions
def get_branch_type(String branch_name) {
    def dev_pattern = ".*develop"
    def release_pattern = ".*release/.*"
    def feature_pattern = ".*feature/.*"
    def hotfix_pattern = ".*hotfix/.*"
    def master_pattern = ".*master"
    if (branch_name =~ dev_pattern) {
        return "develop"
    } else if (branch_name =~ release_pattern) {
        return "release"
    } else if (branch_name =~ master_pattern) {
        return "master"
    } else if (branch_name =~ feature_pattern) {
        return "feature"
    } else if (branch_name =~ hotfix_pattern) {
        return "hotfix"
    } else {
        return null;
    }
}

pipeline {
  agent {
    docker {
      image 'cypress/base:10'
    }
  }
  tools {nodejs "node"}
  stages {
    stage('Preflight') {
      steps {
        echo "====++++Preflight++++===="
        sh 'node -v'
        sh 'npm --version'
        sh 'rm -rf node_modules'
        script {
          env.BRANCH_TYPE = get_branch_type(env.GIT_BRANCH);
        }
        echo env.BRANCH_TYPE
        sh 'npm install'
      }
    }
    // stage('Test') {
    //   steps {
    //     sh 'npm run test:ui'
    //   }
    // }
    stage('Step 1'){
      steps {
        script {
          if (env.BRANCH_TYPE == 'develop'){
            echo "====++++ I'm develop ++++===="
            // isHotfix = sh (script: "git log -1 | grep 'hotfix'", returnStatus: true)
            // if (isHotfix === 0) {
            //   echo "is an Hotfix"
            //   sshagent(credentials:['dip-jenkins']) {
            //     sh 'git checkout master'
            //     sh 'git merge <hotfix-name>'
            //     sh 'git push --set-upstream origin master'
            //     sh 'git branch -D <hotfix-name>'
            //   }
            // }
          }
          if (env.BRANCH_TYPE == 'master'){
            echo "====++++ I'm master ++++===="
          }
          if (env.BRANCH_TYPE == 'hotfix'){
            echo "====++++ I'm an hotfix ++++===="
          }
          if (env.BRANCH_TYPE == 'release'){
            echo "====++++ I'm a release ++++===="
          }
          if (env.BRANCH_TYPE == 'feature'){
            echo "====++++ I'm a feature ++++===="
          }
        }
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
