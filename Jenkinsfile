pipeline {
    agent any

    stages {
        stage('Hello') {
            steps {
                echo 'Hello World'
            }
        }
        stage('Build'){
            agent{
                docker{
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps{
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
        stage('test'){
            steps{
                sh '''
                ls -la
                if find build -name "index.html" | grep -q .; then
                echo "yes available"
                else
                echo "no not available"
                fi
                npm test

                '''
            }
        }
    }
}