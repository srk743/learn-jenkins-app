pipeline {
    agent any

    stages {
        stage('Build') {
            agent {
                Docker {
                    image 'nod:18-alpine'
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
                '''
            }
        }
    }
}