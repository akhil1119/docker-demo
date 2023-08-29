pipeline {
    agent any 
    environment {
    DOCKERHUB_CREDENTIALS = credentials('docker-hub-asakhil')
    }
    stages { 
        stage('SCM Checkout') {
            steps{
            git 'https://github.com/akhil1119/docker-demo.git'
            }
        }

        stage('Build docker image') {
            steps {  
                sh 'docker build -t asakhil/nodeapp1:$BUILD_NUMBER .'
            }
        }
        stage('login to dockerhub') {
            steps{
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage('push image') {
            steps{
                sh 'docker push asakhil/nodeapp1:$BUILD_NUMBER'
            }
        }
        stage('pull image') {
            steps{
                sh 'docker pull asakhil/nodeapp1:$BUILD_NUMBER'
            }
        }
      stage('run image') {
            steps{
                sh 'docker run -d -p 8080:80 asakhil/nodeapp1:$BUILD_NUMBER'
            }
        }   
}
post {
        always {
            sh 'docker logout'
        }
    }
}

