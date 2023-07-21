pipeline {
    agent any

    stages {
        stage('Checkout SCM') {
            steps {
                // Checkout the Jenkinsfile from the Git repository
               git 'https://github.com/Gowtham-Attili/sim.git'
            }
        }

        stage('Pull and Run Docker Image') {
            steps {
                // Pull the latest Docker image
                bat 'docker pull gowtham47/myimage:latest'

                // Stop and remove any existing container
                bat 'docker stop my-container || true'
                bat 'docker rm my-container || true'

                // Run a new container from the latest image
                bat 'docker run --name my-container -d -p 80:8080 gowtham47/myimage:latest'
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                script {
    // Define the Kubernetes namespace and deployment name
    def namespace = 'your-kubernetes-namespace'
    def deploymentName = 'deployment'

    // Authenticate to the Kubernetes cluster using kubeconfig credentials
    def kubeconfig = credentials('ccd0bf50-8dbe-4e81-abc7-2c9ec958e4cc')
//def kubeconfig = '~/.kube/config'
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
    }

    
}
