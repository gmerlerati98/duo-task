pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh '''
                docker build -t gmerlo98/duo-jenk:latest -t gmerlo98/duo-jenk:v${BUILD_NUMBER} .
                '''
            }
        }
        stage('Push') {
            steps {
                sh '''
                docker push gmerlo98/duo-jenk:latest
                docker push gmerlo98/duo-jenk:v${BUILD_NUMBER}
                '''
            }
        }
        stage('Deploy') {
            steps {
                sh'''
                kubectl apply -f ./kubernetes
                kubectl set image deployment/flask flask-container=gmerlo98/duo-jenk:v${BUILD_NUMBER}
                '''
            }
        }
    }
}
