pipeline {
    agent any

    environment {
        AWS_REGION = 'ap-south-1'
        ECR_REPO = '109990058030.dkr.ecr.ap-south-1.amazonaws.com/balu_934729'
        IMAGE_TAG = 'python_image'
    }

    stages {

        stage('git Clone') {
            steps {
                git 'https://github.com/Balarajuvelpula/project-aws-098.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $109990058030.dkr.ecr.ap-south-1.amazonaws.com/balu_934729:$python_image .'
            }
        }

        stage('Login to AWS ECR') {
            steps {
                sh '''
                aws ecr get-login-password --region $ap-south-1\
                | docker login --username AWS --password-stdin 109990058030.dkr.ecr.$ap-south-1.amazonaws.com
                '''
            }
        }

        stage('Push Image to ECR') {
            steps {
                sh '''
                docker tag $109990058030.dkr.ecr.ap-south-1.amazonaws.com/balu_934729:$python_image 109990058030.dkr.ecr.$ap-south-1.amazonaws.com/$109990058030.dkr.ecr.ap-south-1.amazonaws.com/balu_934729:$python_image
                docker push 109990058030.dkr.ecr.$ap-south-1.amazonaws.com/$109990058030.dkr.ecr.ap-south-1.amazonaws.com/balu_934729:$python_image
                '''
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                docker stop myapp || true
                docker rm myapp || true
                docker run -d -p 80:80 --name myapp 109990058030.dkr.ecr.$ap-south-1.amazonaws.com/$109990058030.dkr.ecr.ap-south-1.amazonaws.com/balu_934729:$python_image
                '''
            }
        }
    }
}








