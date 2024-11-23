pipeline {
    agent any
    triggers {
        githubPush()
    }
    stages {
        stage('Checkout') {
            steps {
                script {
                    sh 'git reset --hard'
                    sh "git pull origin main"
                }
            }
        }
        stage('Install Dependencies') {
            steps {
                script {
                    sh '''
                    docker run --rm -v $PWD:/app -w /app node:16-alpine sh -c "npm install --legacy-peer-deps"
                    '''
                }
            }
        }
        stage('Run Unit Tests') {
            steps {
                script {
                    sh '''
                    docker run --rm -v $PWD:/app -w /app node:16-alpine sh -c "npm run test:unit"
                    '''
                }
            }
        }
        stage('Run Integration Tests') {
            steps {
                script {
                    sh '''
                    docker run --rm -v $PWD:/app -w /app node:16-alpine sh -c "npm run test:integration"
                    '''
                }
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    sh 'docker build -t my-react-app .'
                }
            }
        }
        stage('Deploy') {
            steps {
                script {
                    sh '''
                    sudo docker stop react-app || true
                    sudo docker rm react-app || true
                    sudo docker run -d --name react-app -p 80:80 my-react-app
                    sudo docker ps -a
                    sudo docker logs react-app || true
                    '''
                }
            }
        }
    }
    post {
        success {
            echo 'Build, test, and deployment succeeded!'
        }
        failure {
            echo 'Pipeline failed. Check logs for details.'
        }
    }
}