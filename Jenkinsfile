pipeline {
    agent any

    environment {
        IMAGE_NAME = "swagger-ui-custom"
        CONTAINER_NAME = "swagger-ui-container"
    }

    stages {
        stage('Build Docker Image') {
            steps {
                script {
                    bat "wsl docker build -t ${env.IMAGE_NAME} ."
                }
            }
        }

        stage('Run Swagger UI') {
            steps {
                script {
                    bat "wsl docker rm -f ${env.CONTAINER_NAME} || true"
                    bat "wsl docker run -d --name ${env.CONTAINER_NAME} -p 8080:8080 ${env.IMAGE_NAME}"
                }
            }
        }
    }

    post {
        cleanup {
            cleanWs disableDeferredWipeout: true, deleteDirs: true
        }
    }
}
