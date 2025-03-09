pipeline {
    agent any
    stages {
        
         stage('Install Dependencies') {
            steps {
                echo 'Installing dependencies...'
                sh 'npm install'
            }
        }

        stage('Run Tests') {
            steps {
                echo 'Running tests...'
                sh 'npm test'
            }
        }

        stage('Build Package') {
            steps {
                echo 'Building the package...'
                sh 'npm run build'  // Modify if your project uses a different build command
            }
        }
    }
}
