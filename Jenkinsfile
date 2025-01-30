pipeline {
    agent any

    environment {

        IMAGE_NAME = 'alollosh/mywebapp'
        IMAGE_TAG = '${IMAGE_NAME}:latest'
    }

    stages {
        
        stage('Login to Docker Hub') {
            steps {
                script {
                    withCredentials([usernamePassword(credentialsId: 'DOCKERHUBTOKEN', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                        sh "echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin"
                    }
                }
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh "docker build -t new ."
                }
            }
        }

        

        stage('Push to Docker Hub') {
            steps {
                script {
                    sh "docker push $IMAGE_TAG"
                }
            }
        }

        
    }

    post {
        always {
            sh "docker logout"
        }
    }
}
