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
