pipeline {
    agent any
    environment {
        AWS_DEFAULT_REGION = "ap-south-1"
        AWS_CREDENTIALS = credentials('jenkins-aws') // Ensure this is the ID of your AWS credentials in Jenkins
        S3_BUCKET_NAME = 'testing-pipeline11'
    }
    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/Sharry615/s3bucket', branch: 'master'
            }
        }
        stage('Build') {
            steps {
                echo 'Building the website...'
                // Add any build steps if required, for example:
                // sh 'npm install'
                // sh 'npm run build'
            }
        }
        stage('Deploy to S3') {
            steps {
                script {
                    withAWS(credentials: 'jenkins-aws', region: 'ap-south-1') {
                        sh '''
                            echo "Deploying to S3..."
                            aws s3 sync . s3://${S3_BUCKET_NAME} --exclude ".git/*" --exclude "Jenkinsfile"
                        '''
                    }
                }
            }
        }
    }
    post {
        success {
            echo 'Website successfully deployed to S3.'
        }
        failure {
            echo 'Deployment failed.'
        }
    }
}
