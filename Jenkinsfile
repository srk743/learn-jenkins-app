pipeline {
    agent any

    environment{
        NETLIFY_SITE_ID ='9f4b537b-d23d-4321-a37b-e77e8b64fbcd'
        NETLIFY_AUTH_TOKEN = credentials('netlify-token')
    }
    stages {
        stage('Build') {
            agent {
                docker {
                    image 'node:18'
                    reuseNode true
                } 
            }
            steps {
                sh '''

                ls -la
                npm --version
                node --version
                npm ci
                npm run build
                ls -la
                '''
            }
            
        }
        stage ('Test')
        {
            agent {
                docker {
                    image 'node:18'
                    reuseNode true
                } 
            }
            steps{
        sh '''
            test -f build/index.html
            npm test
          
        '''
            }
            
        }

        stage ( 'Deploy')
        {
            agent {

                docker {

                    image 'node:18'
                    reuseNode true
                }
            }

            steps{
                sh '''
                npm install netlify-cli
                node_modules/.bin/netlify --version

                echo "Deploying to poduction. Site ID: $NETLIFY_SITE_ID"
                node_modules/.bin/netlify status
                node_modules/.bin/netlify deploy --dir=build --prod

                '''
            }

        }
        
    }

}