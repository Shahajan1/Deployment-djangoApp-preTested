
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
                    test -f docker-compose.yml
                '''
            }
        }

        stage('Build Docker Image') {
            steps {
                echo 'Building Docker image'

                sh '''
                    docker compose -f docker-compose.yml build
                '''
            }
        }

        stage('Deploy Application') {
            steps {
                echo 'Deploying Todo Application'

                sh '''
                    docker compose -f docker-compose.yml up -d --build --remove-orphans
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
