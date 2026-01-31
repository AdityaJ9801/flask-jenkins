pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Pull code from your repository
                checkout scm
            }
        }

        stage('Install Dependencies') {
            steps {
                // Use 'bat' for Windows Command Prompt
                bat 'pip install -r requirements.txt'
            }
        }

        stage('Run Tests & Coverage') {
            steps {
                // Generates coverage.xml for SonarQube
                bat 'pytest --cov=app --cov-report=xml tests/'
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
