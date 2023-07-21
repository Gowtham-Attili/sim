pipeline {
    agent any

    stages {
        stage('Pull and Run Docker Image') {
    steps {
        // Pull the latest Docker image
        bat "docker pull gowtham47/myimage:latest"

        // Stop and remove the previous container (if exists)
        bat "docker stop my-container || true"
        bat "docker rm my-container || true"

        // Run the Docker container in the background using 'start /B'
        bat "start /B docker run --name my-container -d -p 80:8080 gowtham47/myimage:latest"
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

    // Print the contents of the workspace for debugging purposes
    sh "ls -la ${WORKSPACE}"

    // Print the kubeconfig to ensure it's correctly loaded (optional, for debugging)
    sh "cat ${kubeconfig}"

    // Apply the Kubernetes deployment YAML to deploy the image
    sh "kubectl --kubeconfig=${kubeconfig} --namespace=${namespace} apply -f deployment.yml"
                    bat "start /B docker run --name my-container -d -p 80:8080 gowtham47/myimage:latest"
}

                // Add deployment to Kubernetes as needed
                // This stage is skipped in this example, but you can include your deployment YAML and kubectl commands here.
            }
        }

        // Add more stages as needed for your Jenkins pipeline
        // e.g., Build, Test, etc.
    }
}
