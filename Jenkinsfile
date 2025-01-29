pipeline {
    agent any

    environment {

        IMAGE_NAME = 'alollosh/mywebapp'
        IMAGE_TAG = '${IMAGE_NAME}:${env.GIT_COMMIT}'
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
                    sh "docker build -t $DOCKER_HUB_USER/$IMAGE_NAME:$IMAGE_TAG ."
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
