pipeline {
    agent any

    environment{
        PROJECT_ID = 'c58df395-9a51-46fc-8a9f-900ad7f79764'
    }

    stages {
        stage('Hello world') {
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
                echo 'chnged'
                ls -la
                npm --version
                node --version
                npm ci
                npm run build
                ls -la
                '''
            }
        }
        stage('Staging'){
            steps{
                echo 'Staging env'
            }
        }
        stage('test'){
            agent{
                docker{
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
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