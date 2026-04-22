stage('Deploy') {
    agent {
        docker {
            image 'node:18-alpine'
            reuseNode true
        }
    }
    steps {
        withCredentials([string(credentialsId: 'netlify-token', variable: 'NETLIFY_AUTH_TOKEN')]) {
            sh '''
                npm install -g netlify-cli
                netlify --version

                echo "Deploying to production. Site ID: $NETLIFY_SITE_ID"

                netlify status

                netlify deploy --prod \
                  --dir=build \
                  --no-build \
                  --site=$NETLIFY_SITE_ID \
                  --auth=$NETLIFY_AUTH_TOKEN
            '''
        }
    }
}





