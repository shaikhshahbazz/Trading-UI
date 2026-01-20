pipeline {
    agent any

    environment {
        SKIP_PREFLIGHT_CHECK = "true"
    }

    stages {
        stage('Clean Workspace') {
            steps {
                echo "Cleaning node_modules and lockfile..."
                sh '''
                    cd $WORKSPACE
                    rm -rf node_modules package-lock.json
                '''
            }
        }

        stage('Install Dependencies') {
            steps {
                echo "Installing npm packages..."
                sh 'cd $WORKSPACE && npm install'
            }
        }

        stage('Build Application') {
            steps {
                echo "Building React app..."
                sh 'cd $WORKSPACE && npm run build'
            }
        }

        stage('Run Application') {
            steps {
                echo "Starting app with PM2..."
                sh 'cd $WORKSPACE && pm2 startOrReload ecosystem.config.js'
            }
        }
    }

    post {
        failure {
            echo "Build failed. Check logs above."
        }
        success {
            echo "Build succeeded!"
        }
    }
}
