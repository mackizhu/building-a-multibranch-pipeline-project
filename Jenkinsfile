pipeline {
    agent none
    environment {
        CI = 'true'
    }
    stages {
        stage('Build') {
            agent {
                docker {
                    image 'node:8-alpine'
                    args '-u root:root -p 3000:3000 -p 5000:5000'
                }
            }
            steps {
                sh 'pwd'
                sh 'ls -al'
                sh 'npm install'
            }
        }
        stage('Test') {
            steps {
                sh './jenkins/scripts/test.sh'
            }
        }
        stage('Deliver for development') {
            when {
                branch 'development'
            }
            steps {
                sh './jenkins/scripts/deliver-for-development.sh'
                input message: 'Finished using the web site? (Click "Proceed" to continue)'
                sh './jenkins/scripts/kill.sh'
            }
        }
        stage('Deploy for production') {
            when {
                branch 'production'
            }
            steps {
                sh './jenkins/scripts/deploy-for-production.sh'
                input message: 'Finished using the web site? (Click "Proceed" to continue)'
                sh './jenkins/scripts/kill.sh'
            }
        }
    }
}
