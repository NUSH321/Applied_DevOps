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
                sh "python${PYTHON_VERSION} -m venv ${VENV_NAME}"
                sh ". ${VENV_NAME}/bin/activate"
            }
        }

        stage('Install Dependencies') {
            steps {
                sh "${VENV_NAME}/bin/pip install -r requirements.txt"
            }
        }

        stage('Run Tests') {
            steps {
                sh "${VENV_NAME}/bin/pytest"
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("my-flask-app:${env.BUILD_ID}")
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
            sh "deactivate || true"
            sh "rm -rf ${VENV_NAME}"
        }
    }
}