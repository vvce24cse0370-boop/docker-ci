pipeline {
    agent any

    environment {
        REGISTRY = "localhost:5000"
        IMAGE_NAME = "anil-demo-app"
    }

    stages {
        stage('1. Checkout Code') {
            steps {
                checkout scm
            }
        }

        stage('2. Application Build & Test') {
            steps {
              bat 'python --version'
        bat 'python -m py_compile app.py'
        bat 'python -m pip install -r requirements.txt'
            }
        }

        stage('3. Build & Tag Docker Image') {
            steps {
                bat "docker build -t ${REGISTRY}/${IMAGE_NAME}:${BUILD_NUMBER} -t ${REGISTRY}/${IMAGE_NAME}:latest ."
            }
        }

        stage('4. Push Image to Registry') {
            steps {
                bat "docker push ${REGISTRY}/${IMAGE_NAME}:${BUILD_NUMBER}"
                bat "docker push ${REGISTRY}/${IMAGE_NAME}:latest"
            }
        }
    }

    post {
        success {
            echo "Pipeline succeeded! Image ${REGISTRY}/${IMAGE_NAME}:${BUILD_NUMBER} is available locally and in the registry."
        }
    }
}
