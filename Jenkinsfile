pipeline {
  agent any
  stages {
    stage('Initial') {
      steps {
        echo 'Killing Docker'
        sh 'docker kill service-1 || true'
        sh 'docker rm service-1 || true'
        sh 'docker rm service-1 || true'
        sh 'docker image prune -f || true'
      }
    }
    stage('Deploy Production') {
      when {
        expression {
          BRANCH_NAME ==~ /(master)/
        }
      }
      steps {
        echo 'Deploying'
        sh 'docker build -t muhbayu/nodejs-deploy:${BUILD_NUMBER} .'
        sh 'docker run -d -p 3000:3000 --name service-1 muhbayu/nodejs-deploy:${BUILD_NUMBER}'
      }
    }
    stage('Unit Test') {
      steps {
        def runUnittest = true
        try{
          input 'Run Unit Test?'
        }catch(e){
           runUnittest = false
        }
        if(runUnittest){
            echo 'Unit test here'
        }
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
