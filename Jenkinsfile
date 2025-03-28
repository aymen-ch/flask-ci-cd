pipeline {
    agent any

    environment {
        GIT_CREDENTIALS_ID = 'github-creds' // Change selon tes credentials
    }

    stages {
        stage('Checkout Code') {
            steps {
                git credentialsId: GIT_CREDENTIALS_ID, url: 'https://github.com/ton-utilisateur/flask-ci-cd.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t flask-app .'
            }
        }

        stage('Run with Docker Compose') {
            steps {
                sh 'docker-compose up -d'
            }
        }

        stage('Test Application') {
            steps {
                sh 'curl -f http://localhost:5000'
            }
        }
    }
}
