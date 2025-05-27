pipeline {
    agent any  // Run this pipeline on any available agent

    stages {
        stage('Checkout') { // Stage to checkout the code
            steps {
                git url: 'https://github.com/psc11110/mypythonapp.git', branch: 'master'
                echo 'Code checked out successfully!'
            }
        }

        stage('Setup Python Environment') { // Stage to set up a virtual environment and install dependencies
            steps {
                sh 'python3 --version' // Verify python3 is available
                sh 'python3 -m venv venv' // Create a virtual environment
                sh '. venv/bin/activate && pip install -r requirements.txt' // Activate and install (Linux/macOS)
                echo 'Python environment set up and dependencies installed.'
            }
        }

        stage('Run Tests') { // Stage to run our Python unit tests
            steps {
                sh '. venv/bin/activate && python3 -m unittest discover -s . -p "test_*.py"'
                echo 'Python tests executed.'
            }
        }

        stage('Archive Artifacts') { // Optional: Stage to archive test results or other build artifacts
            steps {
                archiveArtifacts artifacts: 'app.py, test_app.py', followSymlinks: false
                echo 'Relevant files archived.'
            }
        }
    }

    post { // Actions to perform after the pipeline finishes
        always {
            echo 'Pipeline finished.'
            cleanWs() // Clean up the workspace
        }

        success {
            echo 'Pipeline executed successfully! Hooray!'
        }

        failure {
            echo 'Pipeline failed. Please check the logs.'
        }
    }
}

