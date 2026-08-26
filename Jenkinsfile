pipeline {
    agent any

    stages {

        stage('Node Version') {
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
                    if exist build rmdir /s /q build

                    docker run --rm ^
                      -v "%CD%:/app" ^
                      -w /app ^
                      node:18-alpine ^
                      sh -c "npm ci && npm run build"
                '''
            }
        }

        stage('Test') {
            steps {
                bat '''
                    docker run --rm ^
                      -v "%CD%:/app" ^
                      -w /app ^
                      node:18-alpine ^
                      sh -c "npm test -- --watchAll=false"
                '''
            }
        }
    }

    post {
        always {
            junit allowEmptyResults: true, testResults: 'test-results/junit.xml'
        }
    }
}