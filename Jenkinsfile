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
        stage('Connect to kubernetes') {
            steps {
                kubeconfig(caCertificate: 'LS0tLS1CRUdJTiBDRVJUSUZJQ0FURS0tLS0tCk1JSURCVENDQWUyZ0F3SUJBZ0lJWVBRYk9yVUlkYWN3RFFZSktvWklodmNOQVFFTEJRQXdGVEVUTUJFR0ExVUUKQXhNS2EzVmlaWEp1WlhSbGN6QWVGdzB5TlRBek1EZ3hOelEwTVRGYUZ3MHpOVEF6TURZeE56UTVNVEZhTUJVeApFekFSQmdOVkJBTVRDbXQxWW1WeWJtVjBaWE13Z2dFaU1BMEdDU3FHU0liM0RRRUJBUVVBQTRJQkR3QXdnZ0VLCkFvSUJBUUNpcHNBRE1icEVPT0RjUkNaYTFFd1lzaFoxeFkxdWx1QTlNOElvWjFLNXRvMnRpSzFZL1M3Y3hIek4KV2NnUW5JWmZ6V09aWVN2UXZxSGcyZTR0U0ZKaUp5SXZtRXJlUkozZk1VS2hGUXZKMU4xcm1NQzhTSzVGMHkzSQowMWYrMEpISmtNUkNNaEpFVzRXMUVTUE5DdUZwMEJWZjhvaDFDbXFLOVZDK09SSWlEVUZUTllkTThVVDZZMDNvCi9zUE9XTHM1TGdJeStieFNLd08xeEFtNTc4YW45N1VqOEE2dDVCdEt0QjdmVkE4bGlBOXpiVXNmVk5mRFNOaXYKcjJiOUNYOTJzdlhULzFUeldqSjQyM0huWGZQbDFJVXpTRVhXaWp4aEQyY1o4d2g3dHVEN0djd0lxRmh6MENzdAphalJFZTBSY2N4UG5uRGM5ZTYwUUxPalV4R05WQWdNQkFBR2pXVEJYTUE0R0ExVWREd0VCL3dRRUF3SUNwREFQCkJnTlZIUk1CQWY4RUJUQURBUUgvTUIwR0ExVWREZ1FXQkJSYjlqNFJ1cEFtY1FwZjZQclZFcmdHNDZBQlhEQVYKQmdOVkhSRUVEakFNZ2dwcmRXSmxjbTVsZEdWek1BMEdDU3FHU0liM0RRRUJDd1VBQTRJQkFRQlArT29XMVozUgpWWXM1LytZd3ZwSzFXSFNHaC90VkJtOUpZam9WTG5OcHlpeUlRSkhmYkw0OFJBaEVGYy80TS9FRjBOdFVvdEgwClBTcnp4aEFYRGIzN2lOb3QyUkVnL1BETFVTZCtxTmc3Uy9XeHpiWmZ4TDZOVnJnS2xBZndJSWErVWVENjFST04KN1NoN0t6bGdNSDF2MG9zeTByN0tpNzhwbWpZbkZJbE9CSTMrRGZET2RPaktwdjBkZ1RIdGo2b21HZkFGbDRvMAozZGtOREYyamorZWh5aDZkWkQ3VFUydmhGaGZFbzBWM3QwOFFqS3lQaC9YWUdmR1d4Zmk1L3ZlYlJiRFBCb1lmClV1V21oWVRHeFlMMmVwVlJ4dE14Zk9VMVRRWTJsUGtXQ0Q1eXRpTms4Sm12VU1PNktYZ3MwT1pJWmRwbERJSUsKOG1DZXZXeU1EQjMzCi0tLS0tRU5EIENFUlRJRklDQVRFLS0tLS0K', credentialsId: 'k8-cred', serverUrl: 'https://127.0.0.1:41911') {
    // some block
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
