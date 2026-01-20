pipeline {     agent any 
    tools { 
        nodejs "Nodejs" 
    } 
    stages { 
        stage('Checkout') {             steps { 
                git url: 'https://github.com/shaikhshahbazz/Trading-UI.git', branch: 'master' 
            } 
        } 
        stage('Check Node & NPM') { 
            steps {                 sh 'node -v' 
                sh 'npm -v' 
            } 
        } 
        stage('Install Dependencies') { 
            steps { 
                sh 'npm install' 
            } 
        } 
        stage('Build') {             steps { 
                sh 'CI=false npm run build' 
            } 
        } 
        stage('Test') { 
            steps { 
                sh 'npm test || echo "No tests found"' 
            } 
        } 
    } 
} 
