pipeline {
    agent any
    // {docker { image 'ubuntu:latest' }}
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
                    DOCKER_HOST:tcp://localhost:2376,
                    DOCKER_TLS_VERIFY:1,
                    DOCKER_TLS_CERTDIR:/certs,
                    DOCKER_CERT_PATH:$DOCKER_TLS_CERTDIR/client,
                    DOCKER_BUILDKIT:1,
                    DOCKER_CLI_EXPERIMENTAL:enabled,
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