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
                -t nivedhapm/poc1:latest \
                -t nivedhapm/poc1:build-${BUILD_NUMBER} \
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

        stage('Push Image to Docker Hub') {
            steps {
                withCredentials([
                    usernamePassword(
                        credentialsId: 'dockerhub-creds',
                        usernameVariable: 'DOCKER_USER',
                        passwordVariable: 'DOCKER_PASS'
                    )
                ]) {

                    sh '''
                    echo "$DOCKER_PASS" | docker login -u "$DOCKER_USER" --password-stdin

                    docker push nivedhapm/poc1:latest   

                    docker push nivedhapm/poc1:build-${BUILD_NUMBER}

                    docker logout
                    '''
                }
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