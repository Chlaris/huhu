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
                    ls -la
                    chmod 777 Dockerfile
                    chmod 777 Jenkinsfile
                    ls -la
                    
                    docker build -t nginx-test:v2 .
                    DOCKER_TLS_VERIFY: 0

                '''
            }
        }
        stage('Login') {
            steps {
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage('Push') {
            steps {
                sh 'docker push chlbutler/nginx-test:v2'
            }
        }
    }
    post {
        always {
        sh 'docker logout'
        }
    }
        // stage ('Build image') {
        //     steps {
        //         sh 'docker build -t chlbutler/nginx-test:v2 .'
        //         sh 'docker push chlbutler/nginx-test:v2'
        //         // withDockerRegistry(credentialsId: 'chlbutler-dockerhub', url: 'https://index.docker.io/v1/') {
        //         //     sh 'docker build -t chlbutler/nginx-test:v2 .'
        //         //     sh 'docker push chlbutler/nginx-test:v2'
        //         // }
        //     }
        // }   
}