pipeline {
    agent any

    environment {
        // Define any environment variables if required
        NODE_ENV = 'production'
    }

    stages {
        // Stage 1: Checkout the code from the GitHub repository
        stage('Checkout') {
            steps {
                // Pull the code from the repository
                checkout scm
            }
        }

        // Stage 2: Install dependencies (npm install)
        stage('Install Dependencies') {
            steps {
                script {
                    // Ensure Node.js and npm are available on the agent
                    sh 'npm install'
                }
            }
        }

        // Stage 3: Run tests (using Jest)
        stage('Run Tests') {
            steps {
                script {
                    // Run Jest tests
                    sh 'npm test'
                }
            }
        }

        // Stage 4: Build (create production build if tests pass)
        stage('Build') {
            steps {
                script {
                    // You can add a bundler like Webpack or Babel if needed
                    // For now, we'll just run the application to ensure it's built
                    echo 'Building the application...'
                }
            }
        }

        // Stage 5: Deploy (Optional)
        stage('Deploy') {
            steps {
                script {
                    // Example deploy step: Deploy via SSH to a remote server
                    echo 'Deploying to production server...'
                    // You can use SSH, Docker, or any deployment method (e.g., SCP, FTP)
                    // Example with SSH (make sure the Jenkins node has SSH credentials configured)
                    sh '''
                        ssh -o StrictHostKeyChecking=no user@yourserver.com "cd /var/www/app && git pull origin main && npm install && pm2 restart app"
                    '''
                }
            }
        }
    }

    post {
        // Post-build actions, like notifications
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}
