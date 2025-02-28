pipeline {
    agent any

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/Prajakta713/myflask-app.git'
            }
        }
        stage('Check Python Version') {
            steps {
                bat 'python --version'  // Ensure Python is available
            }
        }
        stage('Setup Environment') {
            steps {
                bat 'python -m venv venv'
                bat '.\\venv\\Scripts\\activate'  // Activate virtual environment
                bat '.\\venv\\Scripts\\pip install -r requirements.txt'  // Install dependencies
            }
        }
        stage('Run Tests') {
            steps {
                bat '.\\venv\\Scripts\\pytest'  // Run tests
            }
        }
        stage('Deploy') {
            steps {
                bat '.\\venv\\Scripts\\python app.py'  // Run the app with Python
                echo 'Application Deployed!'
            }
        }
    }
}
