pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build and Push Docker Compose') {
            steps {
                script {
                    echo 'actually inside stage 2'
                    docker.withRegistry('https://hub.docker.com', 'dockerhub-credentials') {
                        sh 'docker-compose -f docker-compose.yml build'
                        sh 'docker-compose -f docker-compose.yml push'
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
