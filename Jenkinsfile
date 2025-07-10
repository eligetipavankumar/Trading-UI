pipeline {
    agent any

    tools {
        nodejs 'nodejs'  // Make sure this matches the name in Jenkins Global Tool Configuration
    }

    stages {
        stage('Git Checkout') {
            steps {
                // Clone the Node.js project
                git 'https://github.com/eligetipavankumar/Trading-UI.git'
            }
        }

        stage('Install and Build') {
            steps {
                // Install dependencies, fix vulnerabilities, build
                sh 'npm audit fix || true'
                sh 'npm install'
                sh 'npm run build'
            }
        }

        stage('Deploy with PM2') {
            steps {
                // Change to build directory and start the app with PM2
                sh '''
                    cd build
                    pm2 delete Trading-UI || true
                    pm2 start npm --name "Trading-UI" -- start
                '''
            }
        }
    }

    post {
        success {
            echo 'Pipeline executed successfully.'
        }
        failure {
            echo 'Pipeline failed.'
        }
    }
}
