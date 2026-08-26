pipeline {
    agent any

    stages {

        stage('Build') {
            steps {
                bat 'docker run --rm node:18-alpine node --version'
            }
        }

        stage('NPM Version') {
            steps {
                bat 'docker run --rm node:18-alpine npm --version'
            }
        }

        stage('Application Build') {
            steps {
                bat '''
                    docker run --rm node:18-alpine node --version
                    docker run --rm node:18-alpine npm --version
                '''
            }
        }

    }
}