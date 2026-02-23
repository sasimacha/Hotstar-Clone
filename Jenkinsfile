
pipeline {
    agent {
        node {
            label 'AGENT1'
        }
    }

    environment {
        APP_NAME = "Hotstar1"
        NODE_ENV = "production"
    }

    stages {

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Build React App') {
            steps {
                sh '''
                export CI=false
                npm run build
                '''
            }
        }

        stage('Run with PM2') {
            steps {
                sh '''
                pm2 describe $APP_NAME > /dev/null 2>&1 && pm2 delete $APP_NAME || true
                pm2 start "npx serve -s build -l 3000" --name $APP_NAME
                pm2 save
                pm2 status
                '''
            }
        }
    }
}
