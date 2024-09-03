pipeline {
    agent any
   

    stages {
        stage('Build') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true  //gather all file into a signle file for all stages
                }
            }
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

        stage('Test') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true  //gather all file into a signle file for all stages
                }
            }

            steps {
                sh '''
                    test -f build/index.hmtl
                    npm test
                '''
            }
        }
                
    }
}