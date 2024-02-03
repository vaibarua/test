pipeline {
    agent any 

    stages {
        // stage('Checkout') {
        //     steps {
        //         echo 'Checking out code...'
        //         checkout([$class: 'GitSCM', branches: [[name: '*/master']], userRemoteConfigs: [[url: 'https://github.com/vaibarua/test.git']]])
        //     }
        // }


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
                sh 'aws configure list'
                sh 'aws s3 sync ./build s3://react-hosting-test-2'
                echo 'Sync success.'
            }
        }
    }
}
