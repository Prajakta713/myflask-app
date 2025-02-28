pipeline {
    agent any

    environment {
        // Define the path to Python if needed
        PYTHON_PATH = 'C:\\Program Files\\Python313\\python.exe' // Update if Python is installed elsewhere
    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/Prajakta713/myflask-app.git'
            }
        }
        stage('Check Python Version') {
            steps {
                bat "${env.PYTHON_PATH} --version"  // Check Python version
            }
        }
        stage('Setup Environment') {
            steps {
                // Set up virtual environment and install dependencies
                bat "${env.PYTHON_PATH} -m venv venv && .\\venv\\Scripts\\pip install -r requirements.txt"
            }
        }
        stage('Run Tests') {
            steps {
                echo 'No tests defined yet'  // Placeholder for tests
            }
        }
        stage('Deploy') {
            steps {
                // Run the app with Python (ensure correct virtual environment activation)
                bat '.\\venv\\Scripts\\python app.py'  // Ensure the virtual environment is used for running the app
                echo 'Application Deployed!'
            }
        }
    }
}
