pipeline {
    agent none
    environment {
        CI = 'true'
    }
    stages {
        stage('deploy production branch') {
            agent {
                docker {
                    image 'node:8-alpine'
                    args '-u root:root -p 3000:3000 -p 5000:5000'
                }
            }
            when {
                branch 'production'
            }
            steps {
                sh 'pwd'
                sh 'ls -al'
                sh 'npm install'
                sh './jenkins/scripts/test.sh'

                sh './jenkins/scripts/deploy-for-production.sh'
                input message: 'Finished using the web site? (Click "Proceed" to continue)'
                sh './jenkins/scripts/kill.sh'
            }
        }
    }
}
