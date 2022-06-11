pipeline {
    agent {
        docker {
            image 'node:8-alpine'
            args '-u root:root'
        }
    }
    environment {
        CI = 'true'
    }
    stages {
        stage('Build') {
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
    }
}
