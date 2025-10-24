pipeline {
    agent any

    stages {
        stage('Build') {
            agent {
                docker {
                    image 'node:20-alpine'
                    reuseNode true
                }
            }
            steps {
                sh '''
                    ls -la
                    node --version
                    npm --version
                    npm config set strict-ssl false
                    npm ci
                    npm run build
                '''
            }
        }
        stage('Test') {
            agent {
                docker {
                    image 'node:20-alpine'
                    reuseNode true
                }
            }
            steps {
                sh '''
                test -f build/index.html
                npm test
                '''
            }
        }
        stage('E2E Tests') {
            agent {
                docker {
                    image 'mcr.microsoft.com/playwright:v1.56.1-noble'
                    reuseNode true
                }
            }
            steps {
                sh '''
                npm install -g serve
                serve -s build
                npx playwright test
                '''
            }
        }
    }
}
