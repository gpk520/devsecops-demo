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
        stage('Build Docker Image and push ') {
            steps {
                echo 'Building Docker image...'
                sh "docker build -t ${IMAGE_NAME}:${IMAGE_TAG} ." 
                sh "echo 'gpk520@_GPK' | docker login -u 'gpk800' --password-stdin"
                sh "docker push ${IMAGE_NAME}:${IMAGE_TAG}"
            }
        }
 stage('connecting to kubernetes') {
            steps {
              withKubeConfig(caCertificate: '', clusterName: '', contextName: '', credentialsId: 'k8-cred', namespace: 'webapps', restrictKubeConfigAccess: false, serverUrl: 'https://127.0.0.1:35071') {
                   sh "kubectl apply -f kubernetes/deployment.yaml"
                   sh "kubectl get pods"
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
