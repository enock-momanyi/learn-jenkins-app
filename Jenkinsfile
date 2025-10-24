pipeline {
    agent any

    stages {
        stage('Build') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                sh '''
                    ls -la
                    node --version
                    npm --version
                    export NODE_OPTIONS="--max-old-space-size=2048"
                    npm ci || npm install
                    npm run build
                '''
            }
        }
    }
}
