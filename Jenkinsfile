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
                    // sh "docker build -t ${IMAGE_NAME} ."
                        sh 'wsl docker build -t swagger-ui-custom .'
                }
            }
        }

        stage('Run Swagger UI') {
            steps {
                script {
                    sh 'wsl docker rm -f ${CONTAINER_NAME} || true'
                    sh 'wsl docker run -d --name ${CONTAINER_NAME} -p 8080:8080 ${IMAGE_NAME}'
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
