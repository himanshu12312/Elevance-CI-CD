
pipeline {
    agent any

    environment {
        IMAGE_NAME = 'himanshu12107/devops-project:latest'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t "$IMAGE_NAME" ./Docker'
            }
        }

        stage('Test Docker Image') {
            steps {
                sh 'docker run --rm "$IMAGE_NAME" nginx -t'
            }
        }

        stage('Push to Docker Hub') {
            steps {
                withCredentials([
                    usernamePassword(
                        credentialsId: 'dockerhub-creds',
                        usernameVariable: 'DOCKERHUB_USERNAME',
                        passwordVariable: 'DOCKERHUB_TOKEN'
                    )
                ]) {
                    sh '''
                        set +x
                        echo "$DOCKERHUB_TOKEN" | docker login \
                            -u "$DOCKERHUB_USERNAME" --password-stdin
                        docker push "$IMAGE_NAME"
                        docker logout
                    '''
                }
            }
        }
    }

    post {
        success {
            echo 'Docker image built, tested, and pushed successfully!'
        }
        failure {
            echo 'Pipeline failed. Check Console Output for the error.'
        }
    }
}
