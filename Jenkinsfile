pipeline {
    agent any

    environment {
        REPO_URL = 'https://github.com/Jazil26/odoo.git'
        APP_NAME = 'odoo-app'
        CONTAINER_NAME = 'odoo-container'
    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: "${REPO_URL}"
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh 'docker build -t ${APP_NAME}:latest .'
                }
            }
        }

        stage('Stop Existing Container') {
            steps {
                script {
                    sh 'docker stop ${CONTAINER_NAME} || true'
                    sh 'docker rm ${CONTAINER_NAME} || true'
                }
            }
        }

        stage('Run New Container') {
            steps {
                script {
                    sh 'docker run -d --name ${CONTAINER_NAME} -p 8069:8069 ${APP_NAME}:latest'
                }
            }
        }

        stage('Cleanup Old Images') {
            steps {
                script {
                    sh 'docker image prune -f'
                }
            }
        }
    }
}

