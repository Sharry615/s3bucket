pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building..'
            }
        }
        stage('Upload') {
            steps {
                echo 'Testing..'
            }
        }
        stage('Checkout') {
            steps {
                // Checkout the repository from GitHub
                git url: 'https://github.com/Sharry615/s3bucket', branch: 'master'
            }
        }
        stage('Install AWS CLI') {
            steps {
                // Install AWS CLI if not already installed
                sh '''
                if ! command -v aws &> /dev/null
                then
                    curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
                    unzip awscliv2.zip
                    sudo ./aws/install
                fi
                '''
            }
        }
        stage('Copy to S3') {
            steps {
                script {
                    withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', 
                                     credentialsId: 'aws-s3-credentials']]) {
                        sh '''
                        export AWS_ACCESS_KEY_ID=$AWS_ACCESS_KEY_ID
                        export AWS_SECRET_ACCESS_KEY=$AWS_SECRET_ACCESS_KEY

                        # Copy the modified index.html to S3 bucket
                        aws s3 cp index.html s3://testing-pipeline11/index.html
                        '''
                    }
                }
            }
        }
    }
}
