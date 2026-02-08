pipeline {
    agent any
    
    environment {
        APP_NAME = 'python-flask-app'
        DOCKER_REGISTRY = 'docker.io'
        IMAGE_TAG = "${BUILD_NUMBER}"
    }
    
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        
        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("${DOCKER_REGISTRY}/${APP_NAME}:${IMAGE_TAG}")
                }
            }
        }
        
        stage('Test') {
            steps {
                script {
                    echo 'Running tests...'
                    // Add your test commands here
                }
            }
        }
        
        stage('Push Docker Image') {
            steps {
                script {
                    docker.withRegistry('', 'docker-credentials') {
                        docker.image("${DOCKER_REGISTRY}/${APP_NAME}:${IMAGE_TAG}").push()
                    }
                }
            }
        }
    }
    
    post {
        always {
            echo 'Pipeline completed!'
        }
    }
}
