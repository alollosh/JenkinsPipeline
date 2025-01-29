pipeline {
    agent any

    environment {
        DOCKER_HUB_USER = 'alollosh'
        DOCKER_HUB_REPO = 'alollosh/mywebapp'
        IMAGE_NAME = 'mywebapp'
        IMAGE_TAG = 'latest'
    }

    stages {
        

        stage('Build Docker Image') {
            steps {
                script {
                    sh "docker build -t $DOCKER_HUB_USER/$IMAGE_NAME:$IMAGE_TAG ."
                }
            }
        }

        stage('Login to Docker Hub') {
            steps {
                script {
                    withCredentials([usernamePassword(credentialsId: 'DOCKERHUBTOKEN', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                        sh "echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin"
                    }
                }
            }
        }

        stage('Push to Docker Hub') {
            steps {
                script {
                    sh "docker push $DOCKER_HUB_USER/$IMAGE_NAME:$IMAGE_TAG"
                }
            }
        }

        stage('Cleanup') {
            steps {
                sh "docker rmi $DOCKER_HUB_USER/$IMAGE_NAME:$IMAGE_TAG || true"
            }
        }
    }

    post {
        always {
            sh "docker logout"
        }
    }
}
