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
                sh 'python3 -m venv venv'
                sh './venv/bin/pip install -r requirements.txt'
            }
        }
        stage('Run Tests') {
            steps {
                echo 'No tests defined yet'
            }
        }
        stage('Deploy') {
            steps {
                sh 'nohup python3 app.py &'
                echo 'Application Deployed!'
            }
        }
    }
}
