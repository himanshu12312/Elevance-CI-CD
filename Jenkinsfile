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
                sh 'sudo docker build -t elevance-cicd ./Docker'
            }
        }

        stage('Verify Docker Image') {
            steps {
                sh 'sudo docker images'
            }
        }
    }
}