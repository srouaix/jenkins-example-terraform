pipeline {
  agent any
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
    stage('terraform plan') {
      steps {
        sh 'terraform init -no-color'
        sh "terraform plan --out plan -no-color"

        
      }
    }


    stage ("deploy") {
        input {
            message 'Apply ?'
        }
      steps {
            sh "terraform apply plan -auto-approve -no-color"
       }
    }
    }
    post {
        always {
        cleanWs()
        }
    }

}
