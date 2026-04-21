pipeline {
    agent any

    environment {
        ACCOUNT_ID = "109990058030"
        IMAGE_TAG = "python_image"
        REPO_NAME = "balu_934729"
        AWS_REGION = "ap-south-1"
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
                docker build -t ${balu_934729}:${python_image} .
                """
            }
        }

        stage('Login to AWS ECR') {
            steps {
                sh """
                aws ecr get-login-password --region ${ap-south-1} \
                | docker login --username AWS --password-stdin ${109990058030.dkr.ecr.ap-south-1.amazonaws.com}
                """
            }
        }

        stage('Tag Docker Image') {
            steps {
                sh """
                docker tag ${balu_934729}:${python_image} ${109990058030.dkr.ecr.ap-south-1.amazonaws.com}/${balu_934729}:${python_image}
                """
            }
        }

        stage('Push Image to ECR') {
            steps {
                sh """
                docker push ${109990058030.dkr.ecr.ap-south-1.amazonaws.com}/${balu_934729}:${python_image}
                """
            }
        }

        stage('Deploy Container') {
            steps {
                sh """
                docker stop myapp || true
                docker rm myapp || true
                docker run -d -p 80:80 --name myapp ${109990058030.dkr.ecr.ap-south-1.amazonaws.com}/${balu_934729}:${python_image}
                """
            }
        }
    }
}                        
