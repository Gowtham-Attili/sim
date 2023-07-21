pipeline {
    agent any

    stages {
        stage('Pull Docker Image') {
            steps {
                script {
                    // Define the Docker image and tag you want to pull
                    def dockerImage = "gowtham47/myimage:latest"

                    // Pull the Docker image using the 'docker' command
                    bat "docker pull ${dockerImage}"

                    // Log the image details
                    bat "docker images ${dockerImage}"
                }
            }
        }

        // Add more stages as needed for your Jenkins pipeline
        // e.g., Build, Test, Deploy, etc.
    }
}
