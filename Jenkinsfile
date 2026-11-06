pipeline {
    agent any

    stages {

        stage('Build') {
            steps {
                bat 'npm install'
            }
        }

        stage('Test') {
            steps {
                bat 'npm test -- --watchAll=false'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    if (env.BRANCH_NAME == 'main') {
                        bat 'docker build -t nodemain:v1.0 .'
                    } else {
                        bat 'docker build -t nodedev:v1.0 .'
                    }
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    if (env.BRANCH_NAME == 'main') {
                        bat 'docker rm -f nodemain'
                        bat 'docker run -d --name nodemain -p 3000:3000 nodemain:v1.0'
                    } else {
                        bat 'docker rm -f nodedev'
                        bat 'docker run -d --name nodedev -p 3001:3000 nodedev:v1.0'
                    }
                }
            }
        }
    }
}