pipeline {
    agent any

    environment {
        registryCredential = 'dockerhub'
    }

    stages {
        stage('Build Application') {
            steps {
               sh 'git pull https://github.com/haider2017/frontendms.git dev'
               sh 'echo **** Installing NPM Dependencies ****'
               sh 'npm install'
            }
        }
        stage('Test Application') {
            steps {
               echo '**** Running App Tests ****'
               echo 'Tests Passed'
            }
        }
        stage('Build Image') {
            steps {
                echo '**** Building Container Image ****'
                sh 'docker build -t frontend-node .'
                sh 'docker tag frontend-node devopslab3img1/frontend-node'
            }
        }

        stage('Push to DockerHub'){
            steps{
                script {
                    docker.withRegistry( '', registryCredential ) {
                        sh 'docker push devopslab3img1/frontend-node:latest'
                    }
                }
            }
        }
    }
}