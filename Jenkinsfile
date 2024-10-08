pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                // Clone the Git repository containing the Flask application
                git url: 'https://github.com/your-repo/your-flask-youtube-comment-analysis', branch: 'main'
            }
        }

        stage('Set Up Python Environment') {
            steps {
                // Create and activate a Python virtual environment
                sh 'python -m venv venv'
                sh 'source venv/bin/activate'
            }
        }

        stage('Install Dependencies') {
            steps {
                // Install the required Python dependencies
                sh 'venv/bin/pip install -r requirements.txt'
            }
        }

        stage('Run Unit Tests') {
            steps {
                // Run unit tests using unittest
                sh 'venv/bin/python -m unittest discover -s tests'
            }
        }

        stage('Run Application') {
            steps {
                // Run the Flask application (optional, usually for local testing)
                sh 'venv/bin/python app.py'
            }
        }

        stage('Deploy') {
            steps {
                // Add your deployment steps here
                echo 'Deploying application...'
            }
        }
    }

    post {
        always {
            echo 'Pipeline complete!'
            cleanWs()  // Clean workspace after the build
        }
        success {
            echo 'Pipeline succeeded!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}
