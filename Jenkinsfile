pipeline {
    agent any

    environment {
        AWS_REGION = 'us-east-1'
        ECR_REGISTRY = '058664348349.dkr.ecr.us-east-1.amazonaws.com'
        IMAGE_NAME = 'resume-site'
        CONTAINER_NAME = 'resume-app'
    }

    stages {
        stage('Clone Repo'){
            steps{
                script{
                    withCredentials([string(credentialsId: 'github-token', variable: 'GIT_TOKEN')]) {
                        sh '''
                        rm -rf repo || true
                        git clone https://$GIT_TOKEN@github.com/monaliptl/Jenkins-Docker-Flask.git repo
                        '''

                    }
                        
                }
            }

        }

        stage('Build and Push Docker Image') {
            steps {
                script {
                    dir('repo') {
                        withCredentials([[$class: 'AmazonWebServicesCredentialsBinding',credentialsId: 'aws-creds']]) {
                        sh '''
                        aws ecr get-login-password --region $AWS_REGION | docker login --username AWS --password-stdin $ECR_REGISTRY
                        docker build -t $IMAGE_NAME:latest .
                        docker tag $IMAGE_NAME:latest $ECR_REGISTRY/$IMAGE_NAME:latest
                        docker push $ECR_REGISTRY/$IMAGE_NAME:latest
                         ''' 
                        }
                    }
                   
                }
            }
        }

        stage('Run Docker Container') {
            steps {
                script {
                    sh '''
                    docker rm -f $CONTAINER_NAME || true
                    docker run -d -p 80:5000 --name $CONTAINER_NAME $ECR_REGISTRY/$IMAGE_NAME:latest
                    '''
                }
            }
        }
    }
}




