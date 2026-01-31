pipeline {
    agent {
        docker {
            image 'python:3.11'   // Python image with pip
            args '-u root'
        }
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

        stage('Run Tests & Coverage') {
            steps {
                sh 'python -m pytest --cov=app --cov-report=xml tests/'
            }
        }
    }

    post {
        always {
            cleanWs()
        }
    }
}
