pipeline {
    agent any

    stages {

        stage('Install Dependencies') {
            steps {
                echo 'Installing Node dependencies'
                sh 'npm install'
            }
        }

        stage('Unit Test') {
            steps {
                echo 'Running Jest tests'
                sh 'npm test'
            }
        }

        stage('Package') {
            steps {
                echo 'Creating build artifact'

                sh '''
                tar -czf myapp.tar.gz app.js app.test.js package.json package-lock.json
                '''
            }
        }

        stage('Deploy to Test Environment') {
            steps {
                echo 'Deploying to test environment'

                sh '''
                mkdir -p /tmp/test-env
                cp myapp.tar.gz /tmp/test-env/
                '''
            }
        }

        stage('Manual Approval') {
            steps {
                input message: 'Approve deployment to production?'
            }
        }

        stage('Deploy to Production') {
            steps {
                echo 'Deploying to production environment'

                sh '''
                mkdir -p /tmp/prod-env
                cp myapp.tar.gz /tmp/prod-env/
                '''
            }
        }
    }
}
