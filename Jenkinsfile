pipeline {
    agent any

    environment {
        PYTHON_PATH = '"C:\\Program Files\\Python313\\python.exe"'
    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/Prajakta713/myflask-app.git'
            }
        }

        stage('Check Python Version') {
            steps {
                bat "${env.PYTHON_PATH} --version"
            }
        }

        stage('Setup Environment') {
            steps {
                bat """${env.PYTHON_PATH} -m venv venv && .\\venv\\Scripts\\pip install -r requirements.txt"""
            }
        }

        stage('Run Tests') {
            steps {
                echo 'No tests defined yet'
            }
        }

        stage('Deploy') {
            steps {
                script {
                    echo 'Starting Flask app...'

                    // Run Flask app in the foreground
                    bat '.\\venv\\Scripts\\python app.py'

                    // After Flask starts, proceed to run ngrok
                    echo 'Flask app started. Starting ngrok...'

                    // Start ngrok to expose Flask app
                    bat 'ngrok http 5000'

                    // Allow time for ngrok to establish the tunnel
                    sleep(time: 5, unit: 'SECONDS')

                    // You can remove this if not necessary
                    echo 'Flask app is deployed and accessible via ngrok.'
                }
            }
        }
    }
}
