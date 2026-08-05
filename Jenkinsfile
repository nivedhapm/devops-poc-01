pipeline {

    agent any

    environment {
        IMAGE_NAME = "devops-poc-01"
        IMAGE_TAG = "build-${BUILD_NUMBER}"
    }

    stages {

        stage('Checkout Source') {
            steps {
                checkout scm
            }
        }

        stage('Verify Project Structure') {
            steps {
                sh '''
                echo "Checking project structure..."
                ls -R
                '''
            }
        }

        stage('Verify Website Files') {
            steps {
                sh '''
                test -f website/index.html
                test -f website/style.css
                echo "Website files verified."
                '''
            }
        }

        stage('Build Docker Image') {
            steps {
                sh '''
                docker build \
                -t ${IMAGE_NAME}:${IMAGE_TAG} \
                -f docker/Dockerfile .
                '''
            }
        }

        stage('List Docker Images') {
            steps {
                sh '''
                docker images
                '''
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