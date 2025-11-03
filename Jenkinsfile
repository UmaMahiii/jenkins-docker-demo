pipeline {
    agent any

    environment {
        IMAGE_NAME = "jenkins-docker-demo"
    }

    stages {
        stage('Clone Repository') {
            steps {
                echo 'Cloning repository...'
                git branch: 'main', url: 'https://github.com/UmaMahiii/jenkins-docker-demo.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                echo 'Building Docker image...'
                bat "docker build -t %IMAGE_NAME% ."
            }
        }

        stage('Run Container') {
            steps {
                echo 'Stopping and removing any existing container...'
                bat '''
                docker stop %IMAGE_NAME% || echo "No container to stop"
                docker rm %IMAGE_NAME% || echo "No container to remove"
                '''

                echo 'Running new Docker container on port 8081...'
                bat "docker run -d -p 8081:8080 --name %IMAGE_NAME% %IMAGE_NAME%"
            }
        }

        stage('Verify Container') {
            steps {
                echo 'Verifying container is running...'
                bat 'docker ps'
            }
        }
    }

    post {
        success {
            echo '✅ Pipeline executed successfully!'
        }
        failure {
            echo '❌ Pipeline failed. Check logs for errors.'
        }
    }
}
