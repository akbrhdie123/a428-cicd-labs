pipeline {
    agent {
        docker {
            image 'node:16-buster-slim'
            args '-p 3000:3000'
        }
    }
    stages {
        stage('Build') {
            steps {
                sh 'npm install'
            }
        }
        stage('Test') {
            steps {
                sh './jenkins/scripts/test.sh'
            }
        }
        stage('Approve based on environment lead') {
            steps {
                input message: 'Ingin Melanjutkan Ke Tahap Deployment?', ok: 'Proceed', submitter: 'users'
            }
        }
        stage('Deploy') { 
            steps {
                sh './jenkins/scripts/deliver.sh' 
                sh './jenkins/scripts/kill.sh' 
                sh 'sleep 10' 
            }
        }
    }
}
