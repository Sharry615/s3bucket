pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building..'
            }
        }
        stage('upload') {
            steps {
                echo 'Testing..'
            }
        }
         stage('Deploy') {
            steps {
                withAWS(region: 'ap-south-1', credentials:'suresh') {
                    sh 'ls -la'
                    sh 'aws s3 cp . s3://testing-pipeline11/index.html
            }
        }
    }
}
