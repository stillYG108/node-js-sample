pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "nodejs-heroku-sample:latest"
        CONTAINER_NAME = "nodejs-app"
    }

    stages {
        stage('Build Docker Image') {
            steps {
                script {
                    echo "Building Docker image..."
                    docker.build(DOCKER_IMAGE)
                }
            }
        }

        stage('Run Docker Container') {
            steps {
                script {
                    echo "Stopping old container (if exists)..."
                    sh "docker rm -f ${CONTAINER_NAME} || true"

                    echo "Starting new container..."
                    sh "docker run -d -p 3000:5000 --name ${CONTAINER_NAME} ${DOCKER_IMAGE}"

                    echo "Container logs:"
                    sh "docker logs ${CONTAINER_NAME}"
                }
            }
        }
    }

    post {
        always {
            echo '✅ CI/CD Pipeline Finished'
        }
    }
}
