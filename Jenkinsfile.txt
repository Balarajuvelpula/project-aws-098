pipeline {
    agent any
    
    tools {
        maven 'maven3.6'
        jdk 'jdk17'
    }

    stages {
        stage('git checkout') {
            steps {
               git branch: 'main',url: 'https://github.com/devopswithkrishnareddy/Boardgame.git'
            }
        }
        stage('compile') {
            steps {
                sh 'mvn compile'
            }
        }
        stage('test') {
            steps {
               sh 'mvn test'
            }
        }
        stage('package') {
            steps {
                sh 'mvn package'
            }
        }
    }
}
