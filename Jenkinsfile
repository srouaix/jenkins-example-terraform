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
        sh 'terraform init'
        sh "terraform plan --out plan"

        
      }
    }

    stage ("deploy") {
      steps {
        def deploy_validation = input(
            id: 'Deploy',
            message: 'Let\'s continue the deploy plan',
            type: "boolean")
        sh 'terraform apply plan -auto-approve -no-color'
    }
  }
  post {
    always {
      cleanWs()
    }
  }
}
}
