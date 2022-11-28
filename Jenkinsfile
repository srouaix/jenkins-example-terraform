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
        input {
            message 'Apply ?'
            parameters {
                booleanParam(name: 'TERRAFORM_APPLY', defaultValue: false, description: 'Apply terrfaorm plan')
            }
        }
      steps {
        script {
            if (TERRAFORM_APPLY.toBoolean()) {
                terraform apply plan -auto-approve -no-color
            }
            else {
                echo "Cancel Apply"
            }
        }

       
        }
    }
    }
    post {
        always {
        cleanWs()
        }
    }

}
