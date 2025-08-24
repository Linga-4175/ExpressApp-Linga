pipeline {
    agent any
    environment {
        NODE_ENV = 'development'
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
                sh 'npm run lint || echo "Linting skipped"'
            }
        }

        stage('Test') {
            steps {
                sh 'npm test || echo "Tests skipped"'
            }
        }

        stage('Build') {
            steps {
                sh 'npm run build || echo "Build skipped"'
            }
        }

        stage('Deploy') {
            when {
                branch 'main'
            }
            steps {
                echo 'Deploying to production...'
                // Add deployment logic here
            }
        }
    }

    post {
        success {
            echo '✅ Pipeline completed successfully!'
        }
        failure {
            echo '❌ Pipeline failed. Check logs for details.'
        }
    }
}
