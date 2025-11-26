pipeline {
    agent {
        docker {
            image 'node:18-alpine'
            image 'mcr.microsoft.com/playwright:v1.57.0-noble'
            reuseNode true
        }
    }
    stages {
    /*
        stage('Build') {
            steps {
                sh '''
                    ls -la
                    node --version
                    npm --version
                    npm ci
                    npm run build
                    ls -la
                '''
            }
        }
    */
        stage('Test') {
            steps {
                echo 'Test stage'
                sh '''
                    test -f build/index.html
                    npm test
                '''
            }
        }

        stage('E2E') {
            steps {
                echo 'Test stage'
                sh '''
                    npm install -g serve
                    serve -s build
                    npx playwright test
                '''
            }
        }
    }

    post {
        always {
            junit 'test-results/junit.xml'
        }
    }
}
