pipeline {
    agent any

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/Prajakta713/myflask-app.git'
            }
        }
        stage('Setup Environment') {
            steps {
                bat 'python -m venv venv'  // Use bat instead of sh on Windows
                bat '.\\venv\\Scripts\\pip install -r requirements.txt'  // Adjusted for Windows path
            }
        }
        stage('Run Tests') {
            steps {
                echo 'No tests defined yet'
            }
        }
        stage('Deploy') {
            steps {
                bat 'start python app.py'  // Use bat for running Python script in the background
                echo 'Application Deployed!'
            }
        }
    }
}
