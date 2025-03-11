pipeline {
    agent any
    environment {
        IMAGE_NAME = 'gpk800/your-image-name'
        IMAGE_TAG = 'latest'  // Use `BUILD_NUMBER` for unique tags
        REGISTRY = 'https://index.docker.io/v1/'  // Change for AWS ECR or GCR
    }
    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/gpk520/devsecops-demo.git'
            }
        }
        stage('Build Docker Image') {
            steps {
                echo 'Building Docker image...'
                sh "docker build -t ${IMAGE_NAME}:${IMAGE_TAG} ." 
            }
        }

        stage('Trivy Security Scan') {
            steps {
                echo 'Running Trivy vulnerability scan...'
                sh "trivy image --exit-code 0 --severity HIGH,CRITICAL ${IMAGE_NAME}:${IMAGE_TAG}"
            }
        }

        stage('Login to Docker Registry') {
            steps {
                echo 'Logging in to Docker Hub...'
                withCredentials([string(credentialsId: 'dockerhubpwd', variable: 'dockerhubpwd')]) {
                sh 'docker Login -u gpk800 -p ${dockerhubpwd}'
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                echo 'Pushing Docker image to registry...'
                sh "docker push ${IMAGE_NAME}:${IMAGE_TAG}"
            }
        }
    }
}
