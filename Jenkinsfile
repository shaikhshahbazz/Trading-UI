pipeline {
    agent any

    tools {
        nodejs 'Node18'
    }

    stages {

        stage('Checkout') {
            steps {
                git url: 'https://github.com/shaikhshahbazz/Trading-UI.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Build') {
            steps {
                sh 'npm run build'
            }
        }

        stage('Validate Build') {
            steps {
                sh 'ls -l'
            }
        }
    }

    post {
        success {
            echo 'UI Build Successful!'
        }
        failure {
            echo 'UI Build Failed!'
        }
    }
}
