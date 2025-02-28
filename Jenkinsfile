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
                    bat """start /b .\\venv\\Scripts\\python app.py"""  // Run Flask app in the background

                    // Step 2: Wait for Flask app to start (allow time for it to initialize)
                    sleep(time: 5, unit: 'SECONDS')

                    // Step 3: Start ngrok to expose Flask app to the internet (port 5000)
                    // Using a temporary file to capture ngrok output
                    bat """start /b ngrok http 5000 > ngrok_output.txt"""  // Expose the Flask app using ngrok and capture output

                    // Step 4: Wait for ngrok to establish the tunnel
                    sleep(time: 5, unit: 'SECONDS')

                    // Step 5: Capture the ngrok public URL from the output
                    def ngrokUrl = readFile('ngrok_output.txt').find(/http:\/\/[a-z0-9]+\.ngrok\.io/) // Regex to find the ngrok public URL

                    // Step 6: Open the public ngrok URL in the default browser
                    echo "Ngrok URL: ${ngrokUrl}"
                    bat """start ${ngrokUrl}"""  // Open Flask app in the browser using ngrok's public URL
                    echo 'Application Deployed and Opened in Browser with ngrok!'
                }
            }
        }
    }
}
