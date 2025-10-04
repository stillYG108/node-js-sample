pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "nodejs-heroku-sample:latest"
        CONTAINER_NAME = "nodejs-app"
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: '<your-repo-url>'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    docker.build(DOCKER_IMAGE)
                }
            }
        }

        stage('Run Docker Container') {
            steps {
                script {
                    // Stop old container if running
                    sh "docker rm -f ${CONTAINER_NAME} || true"
                    // Run new container
                    sh "docker run -d -p 3000:5000 --name ${CONTAINER_NAME} ${DOCKER_IMAGE}"
                }
            }
        }
    }

    post {
        always {
            echo 'CI/CD Pipeline Finished'
        }
    }
}
