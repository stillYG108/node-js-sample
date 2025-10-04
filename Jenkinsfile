pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "nodejs-heroku-sample:latest"
        CONTAINER_NAME = "nodejs-app"
    }

    stages {
        // 🟢 Remove or fix this Checkout stage
        stage('Checkout') {
            steps {
                // Jenkins already clones your repo before reading this file
                // So we can either remove this stage or replace the placeholder URL with your real repo URL

                git branch: 'master', url: 'https://github.com/stillYG108/node-js-sample.git'
            }
        }

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
                    echo "Running Docker container..."
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
            echo '✅ CI/CD Pipeline Finished'
        }
    }
}
