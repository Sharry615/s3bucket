pipeline {
    agent any 
    environment {
        AWS_DEFAULT_REGION = "ap-south-1"
        THE_BUTLER_SAYS_SO = credentials('jenkins-aws')
    }
    stages {
        stage('Checkout') {
            steps {
                echo 'Checking out source code...'
                git 'https://github.com/Sharry615/s3bucket' // Your GitHub repository
            }
        }
        stage('Build') {
            steps {
                echo 'Building stage...'
                // Add any build commands here, for example if you use npm or any other build tool
            }
        }
        stage('Remove Old Build and Copy New Build') {
            steps {
                echo 'Removing old build and copying new build...'
                sh '''
                    # Define the directory where the build is stored
                    BUILD_DIR="/var/www/html/pipeline.videostech.cloud/webhosting"
                    
                    # Remove old build
                    if [ -d "$BUILD_DIR" ]; then
                        rm -rf "$BUILD_DIR/*"
                    fi

                    # Copy new build to the directory
                    cp -r ./dist/* "$BUILD_DIR/"
                '''
            }
        }
        stage('Deploy to S3') { 
            steps { 
                echo 'Deploying to S3...'
                sh 'aws s3 cp ./index.html s3://testing-pipeline11' // Update as necessary
            } 
        }
    }
    post {
        success {
            echo 'Pipeline completed successfully.'
        }
        failure {
            echo 'Pipeline failed.'
        }
    }
}
