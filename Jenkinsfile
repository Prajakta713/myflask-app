pipeline {
    agent any

    environment {
        // Define the path to Python if needed (wrap it in double quotes to handle spaces)
        PYTHON_PATH = '"C:\\Program Files\\Python313\\python.exe"' // Update if Python is installed elsewhere
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
                // Run the Flask app in the background
                bat start /b '.\\venv\\Scripts\\python app.py'  // Run Flask app in the background

                // Wait for the Flask app to start (allow some time for it to initialize)
                sleep(time: 5, unit: 'SECONDS')  // Adjust if needed (to give Flask time to start)

                // Open the app in the default browser
                bat 'start http://127.0.0.1:5000'  // This opens the Flask app in the default web browser

                echo 'Application Deployed and Opened in Browser!'
            }
        }
    }
}
