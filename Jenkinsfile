pipeline {
    agent any
    environment {
        DOCKERHUB_CREDENTIALS = credentials('chlbutler-dockerhub')
    }
    stages {
        stage('Clone') {
            steps {
                git credentialsId: 'chlbutler-dockerhub', url: 'https://github.com/Chlaris/huhu.git', branch: 'main'
            }
        }
        stage('Build') {
            steps {
                sh '''
                    docker --version
                    docker ps
                    docker build -t nginx-test:v2 .
                    DOCKER_TLS_VERIFY: 0

                '''
            }
        }
        // stage('Login') {
        //     steps {
        //         sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
        //     }
        // }
        // stage('Push') {
        //     steps {
        //         sh 'docker push chlbutler/nginx-test:v2'
        //     }
        // }
    }
    post {
        always {
        sh 'docker logout'
        }
    }   
}