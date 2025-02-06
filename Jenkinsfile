pipeline {
        agent {
        label 'ecm'
    }

        
    environment {
        IMAGE_NAME = "swagger-ui-custom"
        CONTAINER_NAME = "swagger-ui-container"
    }


        
    stages {
    
        stage('Debug') {
            steps {
                script {
                     echo "Jenkinsfile загружен правильно!"
                 }
            }
        }
    
            

        stage('Build Docker Image') {
            steps {
                script {
                    sh "docker build -t ${IMAGE_NAME} ."
                }
            }
        }

        stage('Run Swagger UI') {
            steps {
                script {
                    sh "docker rm -f ${CONTAINER_NAME} || true"
                    sh "docker run -d --name ${CONTAINER_NAME} -p 8080:8080 ${IMAGE_NAME}"
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
