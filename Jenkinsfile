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
                sh 'docker build -t nodeapp:v1.0 .'
            }
        }

        stage('Deploy') {
            steps {
                script {
                    if (env.BRANCH_NAME == 'main') {
                        // Main branch goes to port 3000
                        sh 'docker rm -f nodemain || true'
                        sh 'docker run -d --name nodemain -p 3000:3000 nodeapp:v1.0'
                    } else {
                        // Dev branch goes to port 3001
                        sh 'docker rm -f nodedev || true'
                        sh 'docker run -d --name nodedev -p 3001:3000 nodeapp:v1.0'
                    }
                }
            }
        }
    }
}