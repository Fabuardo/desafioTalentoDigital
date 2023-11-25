pipeline {
    environment {
        DOCKERHUB_USERNAME = 'fabiantapiatilleria'
        DOCKERHUB_PASSWORD = credentials('DockerHub')
        DOCKERHUB_REPO = 'fabiantapiatilleria/latestNode'
    }

    agent any
    
    stages {
        stage('Checkout') {
            steps {
                script {
                    checkout scm
                }
            }
        }

        stage('Instalacion Dependencias') {
            steps {
                script {
                    sh 'npm install'
                }
            }
        }
        
        stage('Dockerizar') {
            steps {
                script {
                    // Build Docker image
                    sh "docker build -t $DOCKERHUB_REPO:latest ."
                    
                    // Log in to Docker Hub
                    sh "docker login -u $DOCKERHUB_USERNAME -p $DOCKERHUB_PASSWORD"
                    
                    // Push Docker image to Docker Hub
                    sh "docker push $DOCKERHUB_REPO:latest"
                }
            }
        }
    }
}
