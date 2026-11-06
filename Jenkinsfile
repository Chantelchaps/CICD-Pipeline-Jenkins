pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t nodemain:v1.0 .'
            }
        }

        stage('Deploy') {
            steps {
                bat 'docker rm -f nodemain || exit 0'
                bat 'docker run -d --name nodemain -p 3000:3000 nodemain:v1.0'
            }
        }
    }
}