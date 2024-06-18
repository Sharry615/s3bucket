pipeline {
    agent any

    environment {
        AWS_DEFAULT_REGION = 'ap-south-1' // e.g., 'us-east-1'
        S3_BUCKET_NAME = 'testing-pipeline11'
        AWS_CREDENTIALS = credentials('aws-credentials-id') // Jenkins credentials ID for AWS
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Sharry615/s3bucket.git'
            }
        }
        stage('Deploy to S3') {
            steps {
                script {
                    // Clean the S3 bucket before deployment
                    sh """
                    aws s3 rm s3://${S3_BUCKET_NAME} --recursive \
                      --region ${AWS_DEFAULT_REGION} \
                      --profile ${AWS_CREDENTIALS}
                    """
                    
                    // Upload new files to the S3 bucket
                    sh """
                    aws s3 cp . s3://${S3_BUCKET_NAME} --recursive \
                      --region ${AWS_DEFAULT_REGION} \
                      --profile ${AWS_CREDENTIALS}
                    """
                }
            }
        }
    }

    post {
        success {
            echo 'Deployment succeeded!'
        }
        failure {
            echo 'Deployment failed!'
        }
    }
}
