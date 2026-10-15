```groovy
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
                sh 'test -f nginx.conf'
                sh 'test -f style.css'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'sudo docker build -t portfolio:latest .'
            }
        }

        stage('Deploy Container') {
            steps {
                sh 'sudo docker rm -f portfolio || true'
                sh 'sudo docker run -d --name portfolio --restart unless-stopped -p 8081:80 portfolio:latest'
            }
        }

        stage('Verify Deployment') {
            steps {
                sh 'sudo docker ps'
                sh 'sudo docker exec portfolio nginx -t'
                sh 'curl -fsS http://localhost:8081/health'
            }
        }
    }
}
```
