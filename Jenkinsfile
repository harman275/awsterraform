pipeline {
    agent any

    environment {
        // TF_WORKSPACE = 'default' // Name of the Terraform workspace
        // TF_VAR_region = 'us-east-1' // Example of a Terraform variable (e.g., AWS region)
        AWS_ACCESS_KEY_ID = credentials('AWS-Credentials') // AWS Access Key ID from Jenkins credentials
        AWS_SECRET_ACCESS_KEY = credentials('AWS-Credentials') // AWS Secret Access Key from Jenkins credentials
    }

    stages {
        stage('Checkout') {
            steps {
                echo 'Checking out the code from GitHub...'
                // Clone the repository containing the Terraform code
                git branch: 'main', url: 'https://github.com/harman275/awsterraform.git'
            }
        }

        // stage('install Terraform') {
        //     steps {
        //         echo 'Installing the terraform...'
        //         sh '''
        //         sudo apt-get update && sudo apt-get install -y gnupg software-properties-common
        //         wget -O- https://apt.releases.hashicorp.com/gpg | gpg --dearmor | sudo tee /usr/share/keyrings/hashicorp-archive-keyring.gpg > /dev/null
        //         gpg --no-default-keyring --keyring /usr/share/keyrings/hashicorp-archive-keyring.gpg --fingerprint
        //         echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/hashicorp.list
        //         sudo apt update
        //         sudo apt-get install terraform
        //         '''
        //     }
        // }

        stage('Initialize Terraform') {
            steps {
                echo 'Initializing Terraform...'
                // Initialize the Terraform environment
                sh 'terraform init'
            }
        }

        // stage('Validate Terraform') {
        //     steps {
        //         echo 'Validating Terraform configuration...'
        //         // Validate the Terraform files to ensure they are syntactically correct
        //         sh 'terraform validate'
        //     }
        // }

        stage('Plan Terraform') {
            steps {
                echo 'Planning Terraform deployment...'
                sh 'terraform plan -out=tfplan'
            }
        }

        stage('Apply Terraform') {
            steps {
                echo 'Applying Terraform plan...'
                sh 'terraform apply -input=false tfplan'
            }
        }

        // stage('Cleanup') {
        //     steps {
        //         echo 'Cleaning up...'
        //         // Optional: Remove the Terraform plan file
        //         sh 'rm -f tfplan'
        //     }
        // }
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
