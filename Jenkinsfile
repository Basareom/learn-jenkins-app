pipeline {
    agent any

    stages {
        stage('Build') {
            stage('Build') {
            steps {
                bat 'docker run --rm node:18-alpine node --version'
            }
        }

        stage('NPM Version') {
            steps {
                bat 'docker run --rm node:18-alpine npm --version'
            }
            steps {
                sh '''
                   ls -al
                   node --version
                   npm --version
                   npm ci
                   npm run build
                   '''
            }
        }
    }
}