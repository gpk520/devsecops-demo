pipeline {
     agent {
        kubernetes {
            yaml """
            apiVersion: v1
            kind: Pod
            metadata:
              labels:
                some-label: jenkins-agent
            spec:
              containers:
              - name: build-container
                image: maven:3.8.6-openjdk-11
                command: ['cat']
                tty: true
            """
        }
    }
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
        stage('Build Docker Image and push ') {
            steps {
                echo 'Building Docker image...'
                sh "docker build -t ${IMAGE_NAME}:${IMAGE_TAG} ." 
                sh "echo 'gpk520@_GPK' | docker login -u 'gpk800' --password-stdin"
                sh "docker push ${IMAGE_NAME}:${IMAGE_TAG}"
            }
        }
        stage('Connect to kubernetes') {
            steps {
                kubeconfig(credentialsId: 'k8-connect', serverUrl: '') {
}
               
}
            }
        }

    post {
        success {
            echo '✅ Docker image pushed successfully!'
        }
        failure {
            echo '❌ Pipeline failed! Check login & permissions.'
        }
    }
}
