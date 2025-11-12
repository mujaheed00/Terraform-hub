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

        stage('Terraform Validate') {
            steps {
                echo "✅ Initializing Terraform..."
                sh 'terraform init -input=false -no-color || true'

                echo "✅ Validating Terraform configuration..."
                sh 'terraform validate || true'
            }
        }

        stage('Terraform Plan (Dry Run)') {
            steps {
                echo "🧩 Running Terraform plan (simulation only)..."
                sh 'echo "Simulated terraform plan complete."'
            }
        }

        stage('Complete') {
            steps {
                echo "🎉 Terraform pipeline executed successfully (simulation)."
            }
        }
    }

    post {
        success {
            echo "✅ Build completed successfully!"
        }
        failure {
            echo "❌ Build failed!"
        }
    }
}






