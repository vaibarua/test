pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                echo 'Checking out code...'
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], userRemoteConfigs: [[url: 'https://github.com/vaibarua/test.git']]])
            }
        }
        stage("Install") {
            steps {
                sh 'npm ci'
                echo 'Installation success.'
            }
        }
        stage("Build") {
            steps {
                sh 'npm run build'
                echo 'Build success.'
            }
        }
        stage("Sync with S3") {
            steps {
                withCredentials([aws(credentialsId: "aws creds",  accessKeyVariable: 'AWS_ACCESS_KEY_ID', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY')]) {
                     sh 'aws s3 sync ./build s3://react-hosting-test'
                } 
                echo 'Sync success.'
            }
        }
    }
}