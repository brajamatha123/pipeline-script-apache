pipeline {
    agent any

    stages {
        stage('CI') {
            steps {
                sh 'zip -r apache-html-$BUILD_NUMBER.zip *'
                sh 'aws s3 cp apache-html-$BUILD_NUMBER.zip s3://artifactory-cicd-html/'
            }
        }
        stage('CD') {
            steps {
                sh 'rm -fr *'
                sh 'aws s3 cp s3://artifactory-cicd-html/apache-html-$BUILD_NUMBER.zip .'
                sh 'unzip apache-html-$BUILD_NUMBER.zip'
                sh 'scp index.html root@172.31.15.72:/var/www/html/'
            }
        }
    }
}