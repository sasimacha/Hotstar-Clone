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
                sh 'npm install --production'
            }
        }

        stage('Run with PM2') {
            steps {
                sh '''
                pm2 describe Hotstar1> /dev/null 2>&1 && pm2 delete Hotstar1 || true
                pm2 start server.js --name Hotstar1 --update-env
                pm2 save
                pm2 status
                '''
            }
        }
    }
}
