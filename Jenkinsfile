pipeline {
    agent any

    environment {
        AWS_DEFAULT_REGION = 'us-east-1'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'feature', url: 'https://github.com/mujaheed00/Terraform-hub.git'
            }
        }

        stage('Terraform') {
            steps {
                withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', credentialsId: 'aws-creds']]) {
                    sh '''
                        terraform init -input=false -no-color
                        terraform plan -out=tfplan -input=false -no-color
                        terraform apply -auto-approve -input=false -no-color tfplan
                    '''
                }
            }
        }
    }
}






