pipeline {
    agent any
    tools {
        'org.jenkinsci.plugins.docker.commons.tools.DockerTool' '18.09'
    }
    environment {
        DOCKER_CERT_PATH = credentials('id-for-a-docker-cred')
    }

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

        stage('Build') {
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