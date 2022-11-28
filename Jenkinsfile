pipeline {
  agent any
   environment {
        HTTPS_PROXY = 'http://gateway.seb.zscaler.net:80'
        HTTP_PROXY  = 'http://gateway.seb.zscaler.net:80'
   }

  options {
    skipDefaultCheckout(true)
  }
  stages{
    stage('clean workspace') {
      steps {
        cleanWs()
      }
    }
    stage('checkout') {
      steps {
        checkout scm
      }
    }
    stage('terraform') {
      steps {
        sh 'terraform init'
        sh 'terraform apply -auto-approve -no-color'
      }
    }
  }
  post {
    always {
      cleanWs()
    }
  }
}
