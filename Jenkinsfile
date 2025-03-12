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
                kubeconfig(caCertificate: '''MIIE6TCCAtGgAwIBAgIRAI8a5+mfYXAdpX0isbR4/nIwDQYJKoZIhvcNAQELBQAw
DTELMAkGA1UEAxMCY2EwIBcNMjUwMjI2MTM1ODQ0WhgPMjA1NTAyMjYxNDA4NDRa
MA0xCzAJBgNVBAMTAmNhMIICIjANBgkqhkiG9w0BAQEFAAOCAg8AMIICCgKCAgEA
nBQWIlMO8fQ4qE+FSbXD0g45CKat56CacxgdVq04z4UAmzUkJfefLfwGXdkVPgzJ
wWLr1lfEu3Zw6DQ1PFCxwwl9OoTb7jJklVDwL8i5BTv0l0xGRdH4hf4ZkzdmAoU6
679dJMmpgY8jk8gl7IU6gffoSV4iCTin6SpG6X/HsGitF6S2w8AHagdYWk8PJuwl
GTKU/jmaD755+iAA7uiUbhc3H0kzrMzviaAcnyda1T0mROc+I2gxLF9l4Muhqu9E
h3GyIHm7IIcbvrDFZUJL1DS9WHaSndMGggurwLlM5obM5zOYuOMgZeS4Cai5gynh
iZByUv3+FkDAh56LlOu2bGrVFz3oBTm978Qq0J2YhUK4sVqhmmQUafHT35SN8A7a
MWxRVUxBzMux/l8l9JDQHN2XRauzj+Mqqgpo/ZZwEo6dmZOg/tpH7R47BDcn3c3H
vSD0Z0fxsiuq69bkQEFAap58xwT47Vpf08cs+7hTNcjAFfWmmmke7a/qzPQajDnx
IMUJo4jiQSUWuFHixdhBgmdtxBUPFv7jMjAcyeRvgjQW57d5djZC/BWANBeEwB8U
sGEUGNC5Rsm7LDts4xoTuh1+N7nwkWR4+gtlvHsbWNl+c/wWiZ8UNU0N88IgHPPg
NwQoia5S7AE8FCM2MnIVTJZN9yqHgqDbnsgV6x9w6tUCAwEAAaNCMEAwDgYDVR0P
AQH/BAQDAgKkMA8GA1UdEwEB/wQFMAMBAf8wHQYDVR0OBBYEFATvr5QOhchG3FGJ
0df3nqhodLRzMA0GCSqGSIb3DQEBCwUAA4ICAQAy8SfyHw+UUBLvg0d9UcEk20+Y
g76pS3N6PRuAAolRp2YZAza0lz8nqrSjD1vSukjJ2QNJ2mSW8+UcQjEwkAohMxdK
IjmNOY9VK03LVw+RvzUBKagg0AcC+FnOF2bMG2WyIC53912QJYiIO3ga0jJrfLpy
xzf6HZDw4M/JKBALVzsOr14owkLvbRPAH0xzcXpNTbIw6lvSYrzkC/F336UtE+wI
7MopHHnWLoS10SqAn705RuU5jsJu5Z50Am0QV7RIw0RP9DUtRNyyQ1KAFRFfweg3
OmuMA0VE+nF1AD7jeXuQbOZyusf2A02CLFoN1r+MhopuSfgfcBhLCX168h427aoJ
aATOIQKYakye17iOTgU5FWS9A/8Om070oCgFTXbjQ6cs+u0g4W735A2I1ZrM5/iC
lxzk0b0Zd3brMRlEFqk1ARtPDHWsp5duRLxhQoG8lsS7cMAwkRy81DJqh4DEhrqz
S3b/D3yYKgXGxPdTtSjh5MZDqiSTjhIaOQBZkacVswz+QSzxb+GMIvIzrNG9IeCx
CeDrNziXVEBLtL3/tQEc/VJ2iAkB0rEQa6qACwQ9WoQF0vPFPiBy8KOikvXAcKU0
Se8zJNOebh+X+kziTR/frMrLJz9cabt1jtUsB3NA7Z8ys1+yy8RdgsWPhv3nnxLK
01D1KwPb0l67CtQekg==''', credentialsId: 'k8-connect', serverUrl: 'https://127.0.0.1:41911') {
    // some block
}
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
