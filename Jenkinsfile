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
                sh 'sh 'docker build -t elevance-cicd ./Docker''
            }
        }

        stage('Verify Docker Image') {
            steps {
                sh 'docker images'
            }
        }
    }
}