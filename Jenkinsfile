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

        stage('Deploy with Ansible') {
            steps {
                sh '''
                    ansible-playbook \
                    -i /var/lib/jenkins/ansible/inventory
                    /var/lib/jenkins/ansible/playbook.yml
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
