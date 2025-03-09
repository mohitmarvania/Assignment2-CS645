pipeline {
    agent any
    environment {
        DOCKER_IMAGE = "amisha1407/amishafinalnew"
    }
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/mohitmarvania/Assignment2-CS645.git'
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    sh 'docker build -t $DOCKER_IMAGE .'
                }
            }
        }
        stage('Push to Docker Hub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'docker-credentials', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
                    script {
                        sh 'echo $DOCKER_PASSWORD | docker login -u $DOCKER_USERNAME --password-stdin'
                        sh 'docker push $DOCKER_IMAGE'
                    }
                }
            }
        }
        stage('Deploy to Kubernetes') {
            steps {
                script {
                    sh 'kubectl set image deployment/my-app my-app=$DOCKER_IMAGE'
                }
            }
        }
    }
}
