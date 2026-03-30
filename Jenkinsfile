pipeline {
    agent any

    environment {
        ACR_NAME = "546288497088.dkr.ecr.ap-south-1.amazonaws.com/python-ecr"                // ex: baluacr
        IMAGE_NAME = "project-aws-098"
        TAG = "latest"
    }

    stages {

        stage('Clone Code') {
            steps {
                git branch: 'main', url: 'https://github.com/Balarajuvelpula/project-aws-098.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh '''
                docker build -t $ACR_NAME.azurecr.io/$IMAGE_NAME:$TAG .
                '''
            }
        }

        stage('Push Image to ACR') {
            steps {
                sh '''
                docker push $ACR_NAME.azurecr.io/$IMAGE_NAME:$TAG
                '''
            }
        }
    }
}
