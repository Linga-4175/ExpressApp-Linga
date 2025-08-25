pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Linga-4175/ExpressApp-Linga.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("node-express-app")
                }
            }
        }

        stage('Run Container') {
            steps {
                script {
                    sh 'docker stop node-express || true && docker rm node-express || true'
                    sh 'docker run -d --name node-express -p 3000:3000 node-express-app'
                }
            }
        }

        stage('Post-Deploy Test') {
            steps {
                script {
                    sh 'curl --fail http://localhost:3000 || exit 1'
                }
            }
        }
    }

    post {
        success {
            echo 'Deployment Successful!'
        }
        failure {
            echo 'Deployment Failed!'
        }
    }
}
