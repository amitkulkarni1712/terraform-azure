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
        withCredentials([azureServicePrincipal(credentialsId: '72638069-0faa-468f-8b96-bcc88be5343f',
                                    subscriptionIdVariable: 'SUBS_ID',
                                    clientIdVariable: 'CLIENT_ID',
                                    clientSecretVariable: 'CLIENT_SECRET',
                                    tenantIdVariable: 'TENANT_ID')]) {
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
