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
        withCredentials([azureServicePrincipal(
                    credentialsId: 'Jenkins',
                    subscriptionIdVariable: 'ARM_SUBSCRIPTION_ID',
                    clientIdVariable: 'ARM_CLIENT_ID',
                    clientSecretVariable: 'ARM_CLIENT_SECRET',
                    tenantIdVariable: 'ARM_TENANT_ID'
                ), string(credentialsId: 'access_key', variable: 'ARM_ACCESS_KEY')]) {
        sh 'az login --service-principal -u $CLIENT_ID -p $CLIENT_SECRET -t $TENANT_ID'
    }  
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
