pipeline {
    agent any

    environment {
        PYTHON_VERSION = '3.8'
        VENV_NAME = 'venv'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Setup Python') {
            steps {
                bat "python -m venv ${VENV_NAME}"
                bat "${VENV_NAME}\\Scripts\\activate.bat"
            }
        }

        stage('Install Dependencies') {
            steps {
                bat "${VENV_NAME}\\Scripts\\pip install -r requirements.txt"
            }
        }

        stage('Run Tests') {
            steps {
                bat "${VENV_NAME}\\Scripts\\pytest"
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    bat "docker build -t my-flask-app:${env.BUILD_ID} ."
                }
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying... (replace with actual deployment steps)'
            }
        }
    }

    post {
        always {
            bat "${VENV_NAME}\\Scripts\\deactivate.bat"
            bat "rmdir /s /q ${VENV_NAME}"
        }
    }
}