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
        echo 'Killing Docker'
        sh 'docker kill service-1 || true'
        sh 'docker rm service-1 || true'
        sh 'docker rm service-1 || true'
        sh 'docker image prune -f || true'
      }
      steps {
        echo 'Deploying'
        sh 'docker build -t muhbayu/nodejs-deploy:${BUILD_NUMBER} .'
        sh 'docker run -d -p 3000:3000 --name service-1 muhbayu/nodejs-deploy:${BUILD_NUMBER}'
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
