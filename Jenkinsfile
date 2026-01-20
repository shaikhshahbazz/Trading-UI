pipeline {
    agent any

    tools {
        nodejs 'node18'
    }

    stages {

        stage('Checkout SCM') {
            steps {
                checkout scm
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Audit & Fix') {
            steps {
                sh 'npm audit fix || true'
            }
        }

        stage('Build') {
            steps {
                sh 'npm run build || echo "No build step defined"'
            }
        }
    }
}
