pipeline {
    agent any

    environment {
        // Referencing AWS credentials stored in Jenkins with ID 'ABC'
        AWS_ACCESS_KEY_ID = credentials('ABC')
        AWS_SECRET_ACCESS_KEY = credentials('ABC')
    }

    stages {
        stage('Checkout') {
            steps {
                // Check out the code from the repository
                checkout scm
            }
        }

        stage('Build') {
            steps {
                script {
                    echo 'Building the project...'
                    // Your build steps, e.g., Maven, Gradle, etc.
                    // sh 'mvn clean package'
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    // Use AWS credentials to execute AWS CLI commands
                    withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', credentialsId: 'ABC']]) {
                        // Example: Listing S3 buckets
                        sh 'aws s3 ls'
                    }
                }
            }
        }
    }

    post {
        always {
            echo 'Cleaning up...'
            // Clean up actions, such as deleting temporary files or notifying via email
        }
        success {
            echo 'Pipeline succeeded!'
            // Actions to perform on success
        }
        failure {
            echo 'Pipeline failed.'
            // Actions to perform on failure
        }
    }
}


// pipeline {
//     agent any

//     environment {
//         TF_WORKSPACE = 'default' // Name of the Terraform workspace
//         TF_VAR_region = 'us-east-1' // Example of a Terraform variable (e.g., AWS region)
//         AWS_ACCESS_KEY_ID = credentials('ABC') // Stored in Jenkins credentials
//         AWS_SECRET_ACCESS_KEY = credentials('ABC') // Stored in Jenkins credentials
//     }

//     stages {
//         stage('Checkout') {
//             steps {
//                 echo 'Checking out the code from GitHub...'
//                 // Clone the repository containing the Terraform code
//                 git branch: 'main', url: 'https://github.com/your-repo/your-terraform-project.git'
//             }
//         }

//         stage('Initialize Terraform') {
//             steps {
//                 echo 'Initializing Terraform...'
//                 // Initialize the Terraform environment
//                 sh 'terraform init'
//             }
//         }

//         stage('Validate Terraform') {
//             steps {
//                 echo 'Validating Terraform configuration...'
//                 // Validate the Terraform files to ensure they are syntactically correct
//                 sh 'terraform validate'
//             }
//         }

//         stage('Plan Terraform') {
//             steps {
//                 echo 'Planning Terraform deployment...'
//                 // Create a Terraform plan and save it to a file
//                 sh 'terraform plan -out=tfplan'
//             }
//         }

//         stage('Apply Terraform') {
//             steps {
//                 echo 'Applying Terraform plan...'
//                 // Apply the Terraform plan to create/update infrastructure
//                 sh 'terraform apply -input=false tfplan'
//             }
//         }

//         stage('Cleanup') {
//             steps {
//                 echo 'Cleaning up...'
//                 // Optional: Remove the Terraform plan file
//                 sh 'rm -f tfplan'
//             }
//         }
//     }

//     post {
//         always {
//             echo 'Terraform Deployment Process Completed'
//         }

//         success {
//             echo 'Terraform applied successfully!'
//         }

//         failure {
//             echo 'Terraform deployment failed!'
//         }
//     }
// }
