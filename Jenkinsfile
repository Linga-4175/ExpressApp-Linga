pipeline {
    agent any

    environment {
        NODE_ENV = 'development'
        SSH_KEY = credentials('github-ssh-key') // Jenkins credential ID for your SSH key
    }

    stages {
        stage('Checkout') {
            steps {
                sshagent(['github-ssh-key']) {
                    git url: 'git@github.com:Linga-4175/ExpressApp-Linga.git', branch: 'main'
                }
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Lint') {
            steps {
                sh 'npm run lint'
            }
        }

        stage('Test') {
            steps {
                sh 'npm test'
            }
        }

        stage('Build') {
            steps {
                sh 'npm run build'
            }
        }

        stage('Deploy') {
            when {
                branch 'main'
            }
            steps {
                echo 'Deploying to production...'
                // Add deployment script or command here
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed. Check logs for details.'
        }
    }
}
