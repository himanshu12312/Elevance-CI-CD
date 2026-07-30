pipeline {
    agent any

    environment {
        IMAGE_NAME = "himanshu12107/devops-project:latest"
    }

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

        stage('Docker Hub Login') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'dockerhub',
                    usernameVariable: 'DOCKER_USER',
                    passwordVariable: 'DOCKER_PASS'
                )]) {
                    sh '''
                        echo "$DOCKER_PASS" | docker login -u "$DOCKER_USER" --password-stdin
                    '''
                }
            }
        }

        stage('Tag Docker Image') {
            steps {
                sh 'docker tag elevance-cicd $IMAGE_NAME'
            }
        }

        stage('Push Docker Image') {
            steps {
                sh 'docker push $IMAGE_NAME'
            }
        }

        stage('Deploy Application') {
            steps {
                sh '''
                    docker stop elevance-container || true
                    docker rm elevance-container || true

                    docker pull $IMAGE_NAME

                    docker run -d \
                        --name elevance-container \
                        -p 80:80 \
                        $IMAGE_NAME
                '''
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }

        always {
            sh 'docker logout || true'
        }
    }
}