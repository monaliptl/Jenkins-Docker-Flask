pipeline {
    agent any

    environment {
        AWS_REGION = 'us-east-1'
        ECR_REGISTRY = '058664348349.dkr.ecr.us-east-1.amazonaws.com'
        IMAGE_NAME = 'resume-site'
        CONTAINER_NAME = 'resume-app'
    }

    stages {
        stage('Login to ECR') {
            steps {
                script {
                    sh '''
                    aws ecr get-login-password --region $AWS_REGION | docker login --username AWS --password-stdin $ECR_REGISTRY
                    '''
                }
            }
        }

        stage('Pull Docker Image') {
            steps {
                script {
                    sh "docker pull $ECR_REGISTRY/$IMAGE_NAME:latest"
                }
            }
        }

        stage('Run Docker Container') {
            steps {
                script {
                    sh '''
                    docker rm -f CONTAINER_NAME || true
                    docker run -d -p 80:5000 --name resume-site $ECR_REGISTRY/$IMAGE_NAME:latest
                    '''
                }
            }
        }
    }
}


