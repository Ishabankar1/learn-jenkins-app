pipeline {
    agent any

    environment {
        NETLIFY_SITE_ID = '82943bb5-1af0-4bba-aca0-0dc5997f6341'
        NETLIFY_AUTH_TOKEN = credentials ('netlify-token')
    }

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
                    node --version
                    npm --version
                    npm ci
                    npm run build
                    test -f build/index.html
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
                sh '''
                    npm test -- --watch=false
                '''
            }
        }

        stage('Deploy') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                sh '''
                    npm install -g netlify-cli
                    netlify --version
                    echo "Deploying to production. Site ID: $NETLIFY_SITE_ID"
                    node_modules/ .bin/netlify status
                '''
            }
        }
    }
}



