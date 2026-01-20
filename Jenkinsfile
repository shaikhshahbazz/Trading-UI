pipeline {
    agent any

    tools {
        nodejs 'Nodejs'
    }

    stages {

        stage('Git Checkout') {
            steps {
                git 'https://github.com/shaikhshahbazz/Trading-UI.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh '''
                  node -v
                  npm -v
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
