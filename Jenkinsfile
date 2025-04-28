pipeline {
    agent any

    environment {
        GIT_CREDENTIALS = 'github-credentials'  // Name of the credentials
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/sunnysunny280/devops-fullstack-app.git', credentialsId: GIT_CREDENTIALS
            }
        }
        stage('Build') {
            steps {
                sh 'docker-compose build'
            }
        }
        stage('Deploy') {
            steps {
                sh 'docker-compose up -d'
            }
        }
    }
}
