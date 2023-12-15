pipeline {
    agent any

    environment {
        // Define environment variables if needed
        DOCKER_IMAGE_NAME = "mongo-express"
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout the source code from the repository
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    // Build Docker image using Docker command
                    bat "docker build -t ${DOCKER_IMAGE_NAME} ."
                }
            }
        }

        stage('Run Docker Container') {
            steps {
                script {
                    // Run Docker container using Docker command
                    bat "docker run -p 8080:80 --name mongo_express -d ${DOCKER_IMAGE_NAME}"
                }
            }
        }
    }

    post {
        always {
            // Clean up (stop and remove the container) using Docker command
            script {
                bat "docker stop my-container"
                bat "docker rm my-container"
            }
        }
    }
}
