pipeline {
    agent any
    triggers {
        githubPush()
    }
    stages {
        stage('init') {
            steps {
                sh 'npm install'
            }
        }
        stage('unit Tests') {
            steps {
                sh 'npm run test:unit'
            }
        }
        stage('integration Tests') {
            steps {
                sh 'npm run test:integration'
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

/*
stage('build') {
            steps {
                sh 'npm run build'
            }
        }
*/