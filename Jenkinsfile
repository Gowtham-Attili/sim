pipeline {
    agent any

    stages {
        stage('Pull and Run Docker Image') {
            steps {
                script {
                    // Define the Docker image and tag you want to use
                    def dockerImage = "gowtham47/myimage:latest"

                    // Pull the Docker image using the 'docker' command
                    bat "docker pull ${dockerImage}"

                    // Stop and remove the existing container if it exists
                    bat 'docker stop my-container || true'
                    bat 'docker rm my-container || true'

                    // Run the Docker image to create a container in the background
                    def ports = "80:8080"

                    bat "start /B docker run --name my-container -d -p ${ports} ${dockerImage}"
                }
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                script {
                    // Define the Kubernetes namespace and deployment name
                    def namespace = 'your-kubernetes-namespace'
                    def deploymentName = 'deployment'

                    // Authenticate to the Kubernetes cluster using kubeconfig credentials
                    def kubeconfig = credentials('KUBECONFIG_CREDENTIALS_ID')

                    // Apply the Kubernetes deployment YAML to deploy the image
                    sh "kubectl --kubeconfig=${kubeconfig} --namespace=${namespace} apply -f deployment.yml"
                }

                // Add deployment to Kubernetes as needed
                // This stage is skipped in this example, but you can include your deployment YAML and kubectl commands here.
            }
        }

        // Add more stages as needed for your Jenkins pipeline
        // e.g., Build, Test, etc.
    }
}
