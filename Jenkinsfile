pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t elevance-cicd ./Docker'
            }
        }

        stage('Verify Docker Image') {
            steps {
                sh 'docker images'
            }
        }

        stage('Deploy Application') {
            steps {
                sh '''
                docker stop elevance-container || true
                docker rm elevance-container || true
                docker run -d \
                --name elevance-container \
                -p 5000:5000 \
                elevance-cicd
                '''
            }
        }
    }
}