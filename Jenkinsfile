pipeline {
    agent any

    environment {
        // Define your Docker Hub credentials ID (configured in Jenkins)
        DOCKERHUB_CREDENTIALS = credentials('dockerhub-cred')
        // Define the Docker image name and tag
        DOCKER_IMAGE = 'omriyan01/your-docker-image:latest'
    }

    stages {
        stage('Pull Docker Image') {
            steps {
                script {
                    // Authenticate with Docker Hub using the credentials
                    docker.withRegistry('https://registry.hub.docker.com', DOCKERHUB_CREDENTIALS) {
                        // Pull the Docker image
                        docker.image(DOCKER_IMAGE).pull()
                    }
                }
            }
        }

        stage('Run Docker Container') {
            steps {
                script {
                    // Run the Docker container from the pulled image
                    docker.image(DOCKER_IMAGE).run('-d -p 9000:9000')  // Modify the run options as needed
                }
            }
        }
    }

    post {
        success {
            // Cleanup: Stop and remove the Docker container if needed
            script {
                docker.image(DOCKER_IMAGE).stop()
                docker.image(DOCKER_IMAGE).remove(force: true)
            }
        }
    }
}
