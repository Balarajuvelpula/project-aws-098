pipeline {
    agent any

    stages {

        stage('Setup Python Environment') {
            steps {
                sh '''
                sudo apt update
                sudo apt install python3 python3-venv python3-pip -y

                python3 -m venv venv
                . venv/bin/activate

                pip install flask requests
                '''
            }
        }

        stage('Run Application') {
            steps {
                sh '''
                . venv/bin/activate
                python app.py
                '''
            }
        }
    }
}
