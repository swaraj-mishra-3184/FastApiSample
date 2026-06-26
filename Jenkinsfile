pipeline {
    agent any

    environment {
        IMAGE_NAME = "fastapi-sample"
        CONTAINER_NAME = "fastapi-container"
    }

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t ${IMAGE_NAME} .'
            }
        }

        stage('Remove Old Container') {
            steps {
                sh '''
                    docker stop ${CONTAINER_NAME} || true
                    docker rm ${CONTAINER_NAME} || true
                '''
            }
        }

        stage('Run Docker Container') {
            steps {
                sh 'docker run -d --name ${CONTAINER_NAME} -p 8000:8000 ${IMAGE_NAME}'
            }
        }
    }
}