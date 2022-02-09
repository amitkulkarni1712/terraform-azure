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
                credentialsId: '72638069-0faa-468f-8b96-bcc88be5343f',
                subscriptionIdVariable: 'ARM_SUBSCRIPTION_ID',
                clientIdVariable: 'ARM_CLIENT_ID',
                clientSecretVariable: 'ARM_CLIENT_SECRET',
                tenantIdVariable: 'ARM_TENANT_ID')]) {
                        sh """
                        echo "Creating Terraform Plan"
                        "terraform plan -input=false -var-file='terraform.tfvars'"
                        """
                        }
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
