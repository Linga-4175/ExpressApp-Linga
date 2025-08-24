pipeline {
    agent any

    stages {
        stage('Build Docker Image') {
            steps {
                powershell 'docker build -t node-app .'
            }
        }

        stage('Run Container') {
            steps {
                powershell 'docker run -d -p 3000:3000 node-app'
            }
        }
    }
}
