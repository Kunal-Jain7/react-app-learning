pipeline {
    agent any

    stages {
        stage('Build project') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                sh '''
                    ls -ltrh
                    node --version
                    npm --version
                    npm ci
                    npm run build
                    ls -lrth
                '''
            }
        }
        stage('Test') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                echo 'Test stage'
                sh 'test -f build/index.html'
                sh 'npm test'
            }
        }
    }
    post {
        always {
            junit 'test-results/junit.xml'
        }
    }
}