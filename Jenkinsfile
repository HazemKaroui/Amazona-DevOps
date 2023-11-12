pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Login to Docker Registry') {
            steps {
                script {
                    withCredentials([usernamePassword(credentialsId: 'dockerhub-credentials', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
                        sh 'echo $DOCKER_PASSWORD | docker login -u $DOCKER_USERNAME --password-stdin'
                    }
                }
            }
        }

        stage('Build and Push') {
            steps {
                script {
                    sh 'docker-compose -f docker-compose.yml build'
                    sh 'docker-compose -f docker-compose.yml push'
                }
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                script {
                    // Get the list of available Kubernetes contexts
                    def kubeContexts = sh(script: 'kubectl config get-contexts -o name', returnStdout: true).trim()
                    
                    // Iterate over each context and deploy
                    kubeContexts.split().each { context ->
                        echo "Deploying to Kubernetes context: ${context}"
                        
                        // Set Kubernetes context
                        sh "kubectl config use-context ${context}"
                        
                        // Apply Kubernetes deployment and service configurations
                        sh 'kubectl apply -f frontend-deployment.yaml'
                        sh 'kubectl apply -f backend-deployment.yaml'
                        sh 'kubectl apply -f frontend-service.yaml'
                        sh 'kubectl apply -f backend-service.yaml'
                    }
                }
            }
        }
    }

    post {
        success {
            echo 'Pipeline succeeded!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}
