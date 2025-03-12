pipeline {
     agent any
    environment {
        IMAGE_NAME = 'gpk800/your-image-name'
        IMAGE_TAG = 'latest'  // Use `BUILD_NUMBER` for unique tags
        REGISTRY = 'https://index.docker.io/v1/'  // Change for AWS ECR or GCR
        PATH = "$WORKSPACE/bin:$PATH"
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
          stage('Install kubectl') {
            steps {
                sh '''
                mkdir -p $WORKSPACE/bin
                curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
                chmod +x kubectl
                mv kubectl $WORKSPACE/bin/
                kubectl version --client
                '''
            }
        }
        stage('Connect to kubernetes') {
            steps {
                 kubeconfig(caCertificate: '''MIIDBTCCAe2gAwIBAgIIYPQbOrUIdacwDQYJKoZIhvcNAQELBQAwFTETMBEGA1UE
AxMKa3ViZXJuZXRlczAeFw0yNTAzMDgxNzQ0MTFaFw0zNTAzMDYxNzQ5MTFaMBUx
EzARBgNVBAMTCmt1YmVybmV0ZXMwggEiMA0GCSqGSIb3DQEBAQUAA4IBDwAwggEK
AoIBAQCipsADMbpEOODcRCZa1EwYshZ1xY1uluA9M8IoZ1K5to2tiK1Y/S7cxHzN
WcgQnIZfzWOZYSvQvqHg2e4tSFJiJyIvmEreRJ3fMUKhFQvJ1N1rmMC8SK5F0y3I
01f+0JHJkMRCMhJEW4W1ESPNCuFp0BVf8oh1CmqK9VC+ORIiDUFTNYdM8UT6Y03o
/sPOWLs5LgIy+bxSKwO1xAm578an97Uj8A6t5BtKtB7fVA8liA9zbUsfVNfDSNiv
r2b9CX92svXT/1TzWjJ423HnXfPl1IUzSEXWijxhD2cZ8wh7tuD7GcwIqFhz0Cst
ajREe0RccxPnnDc9e60QLOjUxGNVAgMBAAGjWTBXMA4GA1UdDwEB/wQEAwICpDAP
BgNVHRMBAf8EBTADAQH/MB0GA1UdDgQWBBRb9j4RupAmcQpf6PrVErgG46ABXDAV
BgNVHREEDjAMggprdWJlcm5ldGVzMA0GCSqGSIb3DQEBCwUAA4IBAQBP+OoW1Z3R
VYs5/+YwvpK1WHSGh/tVBm9JYjoVLnNpyiyIQJHfbL48RAhEFc/4M/EF0NtUotH0
PSrzxhAXDb37iNot2REg/PDLUSd+qNg7S/WxzbZfxL6NVrgKlAfwIIa+UeD61RON
7Sh7KzlgMH1v0osy0r7Ki78pmjYnFIlOBI3+DfDOdOjKpv0dgTHtj6omGfAFl4o0
3dkNDF2jj+ehyh6dZD7TU2vhFhfEo0V3t08QjKyPh/XYGfGWxfi5/vebRbDPBoYf
UuWmhYTGxYL2epVRxtMxfOU1TQY2lPkWCD5ytiNk8JmvUMO6KXgs0OZIZdplDIIK
8mCevWyMDB33''', credentialsId: 'k8-connect', serverUrl: 'https://127.0.0.1:41911') {
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
