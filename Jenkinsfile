pipeline {
    agent any
    tools {
        terraform 'terraform'
    }
    stages {
    stage('Terraform Init') {
      steps {
        sh "terraform init -input=false"
      }
    }
    stage('Terraform Plan') {
      steps {
        sh "terraform plan -out=tfplan -input=false -var-file='terraform.tfvars'"
      }
    }
    }
}
/*    stage('Terraform Apply') {
      steps {
        input 'Apply Plan'
        sh "terraform apply -input=false tfplan"
      }
    }
    }
}
*/
