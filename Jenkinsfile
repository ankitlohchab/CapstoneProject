pipeline {
    environment {
        USER_CREDENTIALS = credentials('dockerhub')
    }
    agent any
    stages {
        stage('Lint HTML') {
            steps {
                sh 'tidy -q -e *.html'
            }
        }
        stage('Build Docker Image') {
            steps {
                sh 'sudo docker build . -t capstone'
                sh 'sudo docker image ls'
            }
        }
        stage('Push to Docker Hub') {
            steps {
                sh './upload_docker.sh $USER_CREDENTIALS_USR $USER_CREDENTIALS_PSW'
            }
        }
        stage('Deploy') {
            steps {
                sh './create_infra.sh'
            }
        }
    }
}
