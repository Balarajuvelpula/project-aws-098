pipeline {
    agent any

    environment {
        ACCOUNT_ID = "109990058030"
        IMAGE_TAG = "python_image"
        REPO_NAME = "balu_934729"
        ECR_URL = "109990058030.dkr.ecr.ap-south-1.amazonaws.com"
    }

    stages {

        stage('Checkout Code') {
            steps {
                git branch: 'main',
                url: 'https://github.com/Balarajuvelpula/project-aws-098.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh """
                docker build -t ${REPO_NAME}:${IMAGE_TAG} .
                """
            }
        }

        stage('Login to AWS ECR') {
            steps {
                sh """
                aws ecr get-login-password --region ${AWS_REGION} \
                | docker login --username AWS --password-stdin ${ECR_URL}
                """
            }
        }

        stage('Tag Docker Image') {
            steps {
                sh """
                docker tag ${REPO_NAME}:${IMAGE_TAG} ${ECR_URL}/${REPO_NAME}:${IMAGE_TAG}
                """
            }
        }

        stage('Push Image to ECR') {
            steps {
                sh """
                docker push ${ECR_URL}/${REPO_NAME}:${IMAGE_TAG}
                """
            }
        }

        stage('Deploy Container') {
            steps {
                sh """
                docker stop myapp || true
                docker rm myapp || true
                docker run -d -p 80:80 --name myapp ${ECR_URL}/${REPO_NAME}:${IMAGE_TAG}
                """
            }
        }
    }
}                        
