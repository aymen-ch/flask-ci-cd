pipeline {
    agent any

    environment {
        GIT_CREDENTIALS_ID = 'github-creds' // Change selon tes credentials
    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main',credentialsId: GIT_CREDENTIALS_ID	, url: 'https://github.com/aymen-ch/flask-ci-cd.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t flask-app .'
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
