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
                    docker run --rm ^
                    --user root ^
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
                    --user root ^
                    -v "%CD%:/app" ^
                    -w /app ^
                    node:18-alpine ^
                    sh -c "test -f build/index.html && npm test"
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