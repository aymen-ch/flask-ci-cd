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
                bat 'git log -1'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build --no-cache -t flask-app .'
            }
        }

        stage('Run with Docker Compose') {
            steps {
                bat 'docker-compose up -d --force-recreate --remove-orphans'
            }
        }

        stage('Test Application') {
            steps {
                bat 'curl -f http://localhost:5000'
            }
        }
    }
}
