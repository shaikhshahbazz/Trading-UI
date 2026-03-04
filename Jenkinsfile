pipeline {
    agent any

    tools {
        nodejs 'Node16'
    }

    stages {

        stage('Checkout') {
            steps {
                git 'https://github.com/shaikhshahbazz/Trading-UI.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Build') {
            steps {
                sh 'CI=false npm run build'
            }
        }

        stage('Validate Build') {
            steps {
                sh 'ls -l build'
            }
        }
    }

    post {
        failure {
            echo 'UI Build Failed!'
        }
        success {
            echo 'UI Build Successful!'
        }
    }
}
