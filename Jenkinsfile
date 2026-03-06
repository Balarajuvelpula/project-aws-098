pipeline {
    agent any

    stages {

        stage('Clone Repo') {
            steps {
                git branch: 'main', url: 'https://github.com/Balarajuvelpula/project-aws-098.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh '''
                pip3 install flask requests
                '''
            }
        }

        stage('Run Application') {
            steps {
                sh '''
                python3 main.py
                '''
            }
        }

    }
}
