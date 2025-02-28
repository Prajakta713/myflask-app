pipeline {
    agent any

    environment {
        // Define the path to Python if needed (wrap it in double quotes to handle spaces)
        PYTHON_PATH = '"C:\\Program Files\\Python313\\python.exe"' // Update if Python is installed elsewhere
    }

    stages {
        // 1. Pull Latest Code from Git Repository
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/Prajakta713/myflask-app.git'
            }
        }

        // 2. Check Python Version
        stage('Check Python Version') {
            steps {
                bat "${env.PYTHON_PATH} --version"  // Check Python version
            }
        }

        // 3. Set up the Virtual Environment and Install Dependencies
        stage('Setup Environment') {
            steps {
                bat """${env.PYTHON_PATH} -m venv venv && .\\venv\\Scripts\\pip install -r requirements.txt"""
            }
        }

        // 4. Placeholder for Tests (optional if you have tests)
        stage('Run Tests') {
            steps {
                echo 'No tests defined yet'  // Placeholder for tests
            }
        }

        // 5. Deploy and Expose App with ngrok
        stage('Deploy') {
            steps {
                script {
                    // Step 1: Run Flask app in the background
                    // Start the Flask app using the virtual environment's Python
                    bat 'start /b .\\venv\\Scripts\\python app.py'
                    echo 'Flask app started...'

                    // Step 2: Start ngrok to expose the Flask app (port 5000)
                    // Use ngrok to expose the app to the internet
                    bat 'start /b ngrok http 5000'

                    // Optional: Add a small wait to ensure ngrok has time to establish the tunnel
                    sleep(time: 5, unit: 'SECONDS')

                    // Step 3: Open the public ngrok URL in the default browser
                    // Open the Flask app's public URL (this will be shown by ngrok)
                    bat 'start http://127.0.0.1:5000'
                    echo 'Flask app deployed and opened in browser with ngrok!'
                }
            }
        }
    }
}
