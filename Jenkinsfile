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
                    // Assuming 'your-registry-credentials' is the Jenkins credentials ID for Docker registry
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
