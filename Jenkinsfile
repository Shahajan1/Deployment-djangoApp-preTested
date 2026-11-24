
pipeline {
    agent any

    stages {

        stage('Checkout Code') {
            steps {
                echo 'Downloading Todo App from GitHub'
                checkout scm
            }
        }

        stage('Validate Files') {
            steps {
                echo 'Checking project files'

                sh '''
                    ls -la
                    test -f Dockerfile
                    test -f compose.yaml
                '''
            }
        }

        stage('Build Docker Image') {
            steps {
                echo 'Building Docker image'

                sh '''
                    docker compose build
                '''
            }
        }

        stage('Deploy Application') {
            steps {
                echo 'Deploying Todo Application'

                sh '''
                    docker compose up -d --build --remove-orphans
                '''
            }
        }
    }

    post {
        success {
            echo 'Todo App deployed successfully!'
        }

        failure {
            echo 'Deployment failed. Check Jenkins Console Output.'
        }
    }
}
