pipeline {
    agent {
        docker {
            image 'python:3.11'   // Use official Python Docker image
            args '-u root'        // Run as root if you need to install packages
        }
    }

    stages {
        stage('Checkout') {
            steps {
                // Pull code from your repository
                checkout scm
            }
        }

        stage('Install Dependencies') {
            steps {
                // Use 'sh' for Linux shell inside Docker
                sh 'pip install -r requirements.txt'
            }
        }

        stage('Run Tests & Coverage') {
            steps {
                // Using 'python -m' solves most ModuleNotFound issues
                sh 'python -m pytest --cov=app --cov-report=xml tests/'
            }
        }
    }

    post {
        always {
            // Clean up the workspace after completion
            cleanWs()
        }
    }
}
