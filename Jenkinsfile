
pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/jeevanandam1412-beep/Static-portfolio-website-deployed.git'
            }
        }

        stage('Verify Files') {
            steps {
                sh 'ls -la'
                sh 'test -f index.html'
                sh 'test -f Dockerfile'
                sh 'test -f style.css'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t devops-portfolio:latest .'
            }
        }
    }
}
