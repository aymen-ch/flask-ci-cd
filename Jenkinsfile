pipeline {
    agent any

    environment {
        GIT_CREDENTIALS_ID = 'github-creds'
    }

    
    stages {
        stage('Checkout Code') {
            steps {
                cleanWs()
                git branch: 'main', credentialsId: GIT_CREDENTIALS_ID, url: 'https://github.com/aymen-ch/flask-ci-cd.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build --no-cache -t flask-app .'
            }
        }

        stage('Stop and Remove Old Containers') {
            steps {
                bat 'docker stop flask-app || echo "No running container"'
                bat 'docker rm flask-app || echo "No container to remove"'
            }
        }

        stage('Run with Docker Compose') {
            steps {
                bat 'docker-compose up -d --force-recreate'
            }
        }


        stage('Test Application') {
            steps {
                bat 'curl -f http://localhost:5000'
            }
        }
    }
}
