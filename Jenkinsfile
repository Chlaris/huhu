pipeline {
    agent any
    stages {
        stage('Clone') {
            steps {
                git credentialsId: 'nginx-dockerhub', url: 'https://github.com/Chlaris/huhu.git', branch: 'main'
            }
        }
    }
    stage ('Build image') {
        steps {
            withDockerRegistry(credentialsId: 'chlbutler-dockerhub') {
                sh 'docker build -t chlbutler/nginx-test:v2 .'
                sh 'docker push -t chlbutler/nginx-test:v2'
            }
        }
    }
}