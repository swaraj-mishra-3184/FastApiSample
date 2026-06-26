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
                bat "docker build -t %IMAGE_NAME% ."
            }
        }

        stage('Remove Old Container') {
            steps {
                bat '''
                docker stop %CONTAINER_NAME% || exit 0
                docker rm %CONTAINER_NAME% || exit 0
                '''
            }
        }

        stage('Run Docker Container') {
            steps {
                bat "docker run -d --name %CONTAINER_NAME% -p 8000:8000 %IMAGE_NAME%"
            }
        }

    }
}