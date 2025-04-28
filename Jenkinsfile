pipeline {
    agent any
    stages {
        stage('Checkout Code') {
            steps {
                git 'https://github.com/sunnysunny280/devops-fullstack-app.git'
            }
        }
        stage('Build Docker Images') {
            steps {
                sh 'docker-compose build'
            }
        }
        stage('Run App') {
            steps {
                sh 'docker-compose up -d'
            }
        }
    }
}

