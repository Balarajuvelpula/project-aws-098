pipeline {
    agent any

    environment {
        AWS_REGION = "ap-south-1"
        ECR_REGISTRY = "546288497088.dkr.ecr.ap-south-1.amazonaws.com"
        ECR_REPO = "python-ecr"
        IMAGE_TAG = "${BUILD_NUMBER}"
    }

    stages {

        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/Balarajuvelpula/project-aws-098.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh '''
                docker build -t $ECR_REGISTRY/$ECR_REPO:$IMAGE_TAG .
                '''
            }
        }

        stage('Push Image to ECR') {
            steps {
                sh '''
                docker push $ECR_REGISTRY/$ECR_REPO:$IMAGE_TAG
                '''
            }
        }
    }
}
