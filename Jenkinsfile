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
        stage('Run Unit Tests') {
            steps {
                script {
                    sh 'npm run test:unit'
                }
            }
        }
        stage('Run Integration Tests') {
            steps {
                script {
                    sh 'npm run test:integration'
                }
            }
        }
        stage('Start app') {
            steps {
                script {
                    sh 'npm start'
                }
            }
        }
    }
}