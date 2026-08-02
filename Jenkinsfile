pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Git') {
            steps {
                sh 'git --version'
            }
        }

        stage('Java') {
            steps {
                sh 'java -version'
                sh 'javac -version'
            }
        }

        stage('Maven') {
            steps {
                sh 'mvn -version'
            }
        }

        stage('Docker') {
            steps {
                sh 'docker --version'
                sh 'docker info'
            }
        }

        stage('kubectl') {
            steps {
                sh 'kubectl version --client'
                sh 'kubectl get nodes'
            }
        }

        stage('Helm') {
            steps {
                sh 'helm version'
            }
        }

        stage('Kubernetes Health') {
            steps {
                sh 'kubectl cluster-info'
                sh 'kubectl get nodes'
                sh 'kubectl get pods -A'
            }
        }
    }

    post {
        success {
            echo 'DevOps Platform Verification Successful!!'
        }

        failure {
            echo 'Platform Verification Failed.'
        }
    }
}