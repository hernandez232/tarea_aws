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
                    docker run --rm -v /var/lib/jenkins/workspace/pipeline-react:/app -w /app node:16-alpine sh -c "rm -rf node_modules && npm cache clean --force"
                    '''
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

/*
pipeline {
    agent any
    triggers {
        githubPush()
    }
    agent {
        docker { image 'node:16-alpine' }
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
                    sh 'npm install --legacy-peer-deps'
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
/*

/*
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
                    def gitUrl = 'https://github.com/hernandez232/tarea_aws.git'
		            def branch = 'main'
		            sh "git pull origin ${branch}"
                }

            }
        }
        stage('Install Dependencies') {
            steps {
                script {
                    sh 'npm install --legacy-peer-deps'
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
*/

/*
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
*/

/*
stage('build') {
            steps {
                sh 'npm run build'
            }
        }
*/

/*
stage('Start app') {
            steps {
                script {
                    sh 'npm start'
                }
            }
        }
*/