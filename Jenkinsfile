pipeline {
    agent any

    environment {
        # Skip Create React App ESLint preflight check
        SKIP_PREFLIGHT_CHECK = "true"
        NODEJS_HOME = tool name: 'NodeJS', type: 'NodeJSInstallation'
        PATH = "${NODEJS_HOME}/bin:${env.PATH}"
    }

    stages {
        stage('Prepare Workspace') {
            steps {
                echo "Cleaning workspace and fixing permissions..."
                sh '''
                    # Go to workspace
                    cd $WORKSPACE

                    # Ensure Jenkins user owns all files
                    sudo chown -R $(whoami):$(whoami) $WORKSPACE

                    # Remove old node_modules and lockfile
                    rm -rf node_modules package-lock.json
                '''
            }
        }

        stage('Install Dependencies') {
            steps {
                echo "Installing npm dependencies..."
                sh '''
                    cd $WORKSPACE
                    npm install
                '''
            }
        }

        stage('Build Application') {
            steps {
                echo "Building React application..."
                sh '''
                    cd $WORKSPACE
                    npm run build
                '''
            }
        }

        stage('Run Application with PM2') {
            steps {
                echo "Starting application with PM2..."
                sh '''
                    cd $WORKSPACE
                    pm2 startOrReload ecosystem.config.js
                '''
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
