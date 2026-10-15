
pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Verify Files') {
            steps {
                sh '''
                    test -f index.html
                    test -f style.css
                    test -f Dockerfile
                    test -f nginx.conf
                    echo "Project files verified successfully"
                '''
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t devops-portfolio:latest .'
            }
        }

        stage('Run Container') {
            steps {
                sh '''
                    docker rm -f devops-portfolio || true
                    docker run -d --name devops-portfolio -p 8080:80 devops-portfolio:latest
                '''
            }
        }
    }

    post {
        success {
            echo 'Portfolio deployed successfully!'
        }
        failure {
            echo 'Pipeline failed. Check the console output.'
        }
    }
}
```
