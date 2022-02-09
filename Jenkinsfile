pipeline {
    agent any
    tools {
        terraform 'terraform-1.0.10'
    }
    stages {
        stage('Terraform Init') {
            steps {
                sh 'terraform init -input=false'
            }
        }

        stage('Apply') {
            steps {
                sh "terraform apply -input=false tfplan"
            }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: 'tfplan.txt'
        }
    }
}