pipeline {
    agent { label 'agent1' }

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
                bat 'docker build -t jenkins-docker-demo .'
            }
        }

        stage('Run Container') {
            steps {
                echo 'Running Docker container...'
                bat 'docker run -d -p 8080:8080 --name jenkins-docker-demo jenkins-docker-demo'
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
