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
            options {
                timeout(time: 2, unit: 'MINUTES')  // ⏱ stop stage after 2 minutes
            }
            steps {
                withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', credentialsId: 'aws-creds']]) {
                    sh '''
                        set -x
                        terraform init -input=false -no-color || true
                        terraform plan -out=tfplan -input=false -no-color || true
                        terraform apply -auto-approve -input=false -no-color tfplan || true
                    '''
                }
            }
        }
    }

    post {
        always {
            echo "✅ Job completed — pipeline finished execution."
        }
    }
}
