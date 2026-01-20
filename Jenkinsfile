pipeline {
    agent any

    tools {
        nodejs 'node18'
    }

    stages {

        stage('Git Checkout') {
            steps {
                git 'https://github.com/shaikhshahbazz/Trading-UI.git'
            }
        }

        stage('Install npm prerequisites') {
            steps {
                sh '''
                  npm install
                  npm audit fix || true
                '''
            }
        }

        stage('Build Application') {
            steps {
                sh 'npm run build'
            }
        }

        stage('Run Application with PM2') {
            steps {
                sh '''
                  npm install -g pm2
                  pm2 delete Trading-UI || true
                  pm2 start npm --name "Trading-UI" -- start
                  pm2 save
                '''
            }
        }
    }
}
