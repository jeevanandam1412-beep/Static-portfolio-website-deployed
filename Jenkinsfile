
pipeline {
    agent any

    environment {
        AWS_REGION = 'us-east-1'
        ECR_REPOSITORY = '741444304666.dkr.ecr.us-east-1.amazonaws.com/portfolio'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t portfolio:${BUILD_NUMBER} .'
            }
        }

        stage('Login to ECR') {
            steps {
                sh '''
                    aws ecr get-login-password --region $AWS_REGION |
                    docker login --username AWS --password-stdin 741444304666.dkr.ecr.us-east-1.amazonaws.com
                '''
            }
        }

        stage('Tag Image') {
            steps {
                sh '''
                    docker tag portfolio:${BUILD_NUMBER} \
                    ${ECR_REPOSITORY}:${BUILD_NUMBER}
                    docker tag portfolio:${BUILD_NUMBER} \
                    ${ECR_REPOSITORY}:latest
                '''
            }
        }

        stage('Push to ECR') {
            steps {
                sh '''
                    docker push ${ECR_REPOSITORY}:${BUILD_NUMBER}
                    docker push ${ECR_REPOSITORY}:latest
                '''
            }
        }
    }

    post {
        success {
            echo 'Docker image pushed to Amazon ECR successfully!'
        }
        failure {
            echo 'Pipeline failed. Check the stage console output.'
        }
    }
}
