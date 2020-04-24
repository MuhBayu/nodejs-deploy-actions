pipeline {
  agent any
  stages {
    stage('Deploy Production') {
      when {
        expression {
          BRANCH_NAME ==~ /(master|staging|develop|hotfix.*|release.*|feature.*)/
        }
      }
      steps {
        echo 'Deploying'
        sh 'docker build -t muhbayu/nodejs-deploy:${BUILD_NUMBER} .'
        sh 'docker run -d -p 3000:3000 muhbayu/nodejs-deploy:${BUILD_NUMBER}'
      }
    }
    stage('Unit Test') {
      steps {
        input 'Do you approve deployment?'
        echo 'Unit test here'
      }
    }
    stage('Clean') {
      steps {
        echo 'clean'
        sh ''
      }
    }
  }
}
