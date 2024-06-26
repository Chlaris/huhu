pipeline {
    agent any
    // {docker { image 'docker:dind' }}
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
            agent {
                docker {
                    image 'docker:dind'
                    // Run the container on the node specified at the
                    // top-level of the Pipeline, in the same workspace,
                    // rather than on a new node entirely:
                    reuseNode true
                    }
                }
                steps {
                    sh '''
                        docker --version
                        docker ps
                        docker build -t nginx-test:v2 .
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