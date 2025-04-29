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

        stage('Install Dependencies') {
            steps {
                script {
            sh '''
            echo "Docker not found, installing..."
            apt update && apt install -y docker.io curl

            if ! command -v docker-compose &> /dev/null; then
                echo "Docker Compose not found, installing..."
                curl -L "https://github.com/docker/compose/releases/download/v2.19.1/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
                chmod +x /usr/local/bin/docker-compose
            fi

            docker --version
            docker-compose --version
            '''
                    
                    // Install Node.js dependencies if needed (optional)
                    sh 'cd client && npm install'
                    sh 'cd server && npm install'
                }
            }
        }

        stage('Build Docker Images') {
            steps {
                // Build Docker images using docker-compose
                sh 'docker-compose build'
            }
        }

        stage('Run Docker Containers') {
            steps {
                // Start up Docker containers in detached mode
                sh 'docker-compose up -d'
            }
        }

        stage('Clean Up') {
            steps {
                // Optionally clean up resources after the build
                sh 'docker-compose down'
            }
        }
    }
    post {
        always {
            cleanWs() // Clean workspace after the build
        }
    }
}
