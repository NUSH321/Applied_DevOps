pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'youtube-comment-analyzer'
        DOCKER_TAG = "${env.BUILD_NUMBER}"
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'pip install -r requirements.txt'
            }
        }

        stage('Run Tests') {
            steps {
                sh 'python -m pytest'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("${DOCKER_IMAGE}:${DOCKER_TAG}")
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    // Example deployment step - adjust as needed
                    sh "docker-compose up -d"
                }
            }
        }
    }

    post {
        always {
            // Clean up Docker images to save space
            sh "docker rmi ${DOCKER_IMAGE}:${DOCKER_TAG}"
        }
    }
}