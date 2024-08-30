pipeline {
    agent any

    environment {
        TF_WORKSPACE = 'default' // Name of the Terraform workspace
        TF_VAR_region = 'us-east-1' // Example of a Terraform variable (e.g., AWS region)
        AWS_ACCESS_KEY_ID = credentials('ABC') // Stored in Jenkins credentials
        AWS_SECRET_ACCESS_KEY = credentials('ABC') // Stored in Jenkins credentials
    }

    stages {
        stage('Checkout') {
            steps {
                echo 'Checking out the code from GitHub...'
                // Clone the repository containing the Terraform code
                git branch: 'main', url: 'https://github.com/your-repo/your-terraform-project.git'
            }
        }

        stage('Initialize Terraform') {
            steps {
                echo 'Initializing Terraform...'
                // Initialize the Terraform environment
                sh 'terraform init'
            }
        }

        stage('Validate Terraform') {
            steps {
                echo 'Validating Terraform configuration...'
                // Validate the Terraform files to ensure they are syntactically correct
                sh 'terraform validate'
            }
        }

        stage('Plan Terraform') {
            steps {
                echo 'Planning Terraform deployment...'
                // Create a Terraform plan and save it to a file
                sh 'terraform plan -out=tfplan'
            }
        }

        stage('Apply Terraform') {
            steps {
                echo 'Applying Terraform plan...'
                // Apply the Terraform plan to create/update infrastructure
                sh 'terraform apply -input=false tfplan'
            }
        }

        stage('Cleanup') {
            steps {
                echo 'Cleaning up...'
                // Optional: Remove the Terraform plan file
                sh 'rm -f tfplan'
            }
        }
    }

    post {
        always {
            echo 'Terraform Deployment Process Completed'
        }

        success {
            echo 'Terraform applied successfully!'
        }

        failure {
            echo 'Terraform deployment failed!'
        }
    }
}
