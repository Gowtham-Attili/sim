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

                    // Run the Docker image to create a container
                    def containerName = "my-container"
                    def ports = "80:8080"
                    //def volume = "C:/path/to/host/directory:/container/directory"

                    bat "docker run -d --name ${containerName} -p ${ports} ${dockerImage}"
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
            }
        }

        // Add more stages as needed for your Jenkins pipeline
        // e.g., Build, Test, etc.
    }
}
