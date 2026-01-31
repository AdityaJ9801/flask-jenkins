pipeline {
    agent {
        docker {
            image 'python:3.11'
            args '-u root'
            reuseNode true
        }
    }

    environment {
        PYTHONUNBUFFERED = '1'
        HOME = "${WORKSPACE}"
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Setup') {
            steps {
                sh '''
                    apt-get update -qq
                    apt-get install -y git
                    pip install --upgrade pip
                '''
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'pip install -r requirements.txt'
            }
        }

        stage('Run Tests') {
            steps {
                sh 'python -m pytest --cov=app --cov-report=xml --cov-report=html tests/'
            }
        }

        stage('Archive Reports') {
            steps {
                archiveArtifacts artifacts: 'coverage.xml,htmlcov/**', allowEmptyArchive: true
            }
        }
    }

    post {
        always {
            cleanWs(notFailBuild: true)
        }
    }
}
