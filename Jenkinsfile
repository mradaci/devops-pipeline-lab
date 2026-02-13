pipeline {
    agent any
    
    environment {
        IMAGE_NAME = 'devops-website'
        IMAGE_TAG = "${BUILD_NUMBER}"
    }
    
    stages {
        stage('Checkout') {
            steps {
                echo 'Checking out code...'
                checkout scm
            }
        }
        
        stage('Build') {
            steps {
                echo 'Building Docker image...'
                sh "docker build -t ${IMAGE_NAME}:${IMAGE_TAG} ."
                sh "docker tag ${IMAGE_NAME}:${IMAGE_TAG} ${IMAGE_NAME}:latest"
            }
        }
        
        stage('Test') {
            steps {
                echo 'Running tests...'
                sh "docker run --rm ${IMAGE_NAME}:latest nginx -t"
            }
        }
        
        stage('Deploy') {
            steps {
                echo 'Deploying application...'
                sh '''
                    docker stop devops-website || true
                    docker rm devops-website || true
                    docker run -d --name devops-website -p 8081:80 ${IMAGE_NAME}:latest
                '''
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

