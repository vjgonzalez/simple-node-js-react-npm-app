pipeline {
    agent {
        docker {
            image 'node:6-alpine'
            args '-p 3002:3000'
        }
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
    }
}
