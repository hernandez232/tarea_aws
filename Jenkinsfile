pipeline {
    agent any
    triggers {
        githubPush()
    }
    enviroment{
        BUCKET = "awsbucketubuntu"
    }
    stages ('deploy to S3') {
        steps {
            withAWS(credentials: 'aws_ubuntu', region: 'us-east-2'){
                sh 'aws s3 sync . s3://$BUCKET --exclude ".git/*"'
                sh 'aws s3 ls s3://BUCKET'
            }
        }
    }
    stages {
        stages('init') {
            steps {
                sh 'npm install'
            }
        }
        stages('unit Tests') {
            steps {
                sh 'npm run test:unit'
            }
        }
        stages('integration Tests') {
            steps {
                sh 'npm run test:integration'
            }
        }
        stages('Start app') {
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