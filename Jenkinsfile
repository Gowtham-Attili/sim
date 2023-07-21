pipeline {
    agent any

    stages {
        stage('Pull Docker Image') {
            steps {
                script {
                    // Define the Docker image and tag you want to pull
                    def dockerImage = "gowtham47/myimage:latest"

                    // Pull the Docker image using the 'docker' command
                    docker.image(dockerImage).pull()

                    // You can also log the image details if needed
                    docker.image(dockerImage).withRun {
                        echo "Docker image pulled successfully: ${dockerImage}"
                    }
                }
            }
        }

        // Add more stages as needed for your Jenkins pipeline
        // e.g., Build, Test, Deploy, etc.
    }
}
