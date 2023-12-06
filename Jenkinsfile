pipeline {
    agent any
    stages {
        stage('Checkout'){
            steps {
                checkout scm
            }
        }
        stage('Build') {
            steps {
                bat 'npm install'
            }
        }
        stage('Test') {
            steps {
                bat 'npm test'
            }
        }
        stage('Build Image'){
            steps{
                withCredentials([usernamePassword(credentialsId: '6ade19c2-c2dd-406e-849a-a5baf79399b5', passwordVariable: 'pass', usernameVariable: 'user')]) {
                    bat """docker build -t toty8/student-registry-app:%BUILD_ID% .
                           docker login --username %user% --password %pass%
                           docker push toty8/student-registry-app:%BUILD_ID%"""

            }
        }
        }
        stage('Deploy Image'){
            steps{
                withCredentials([usernamePassword(credentialsId: '6ade19c2-c2dd-406e-849a-a5baf79399b5', passwordVariable: 'pass', usernameVariable: 'user')]) {
                    bat """docker pull toty8/student-registry-app:1.0.0
                           docker run -d toty8/student-registry-app:1.0.0"""

            }
        }
        }
    }
}