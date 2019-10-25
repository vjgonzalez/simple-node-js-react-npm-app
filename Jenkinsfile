pipeline {
    agent {
        docker {
            image 'node:6-alpine'
            args '-p 3002:3000'
        }
    }
    environment {
        CI = 'true'
    }
    triggers {
        pollSCM('*/1 * * * *')
    }
    stages {
        stage('Build') { 
            steps {
                sh 'npm install' 
                sh 'npm build'
            }
        }
        stage('Test') {
            steps {
                sh 'npm test'
            }
        }
        stage('Deploy') {
            steps {
                sh './jenkins/scripts/deliver.sh'
                input message: 'Finished using the web site? (Click "Proceed" to continue)'
                sh './jenkins/scripts/kill.sh'
            }
        }
    }
}
