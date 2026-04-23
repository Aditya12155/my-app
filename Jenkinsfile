pipeline {
    agent any

    environment {
        IMAGE_NAME = "adibhai/my-app"    
    }

    stages {

        stage('Clone Source') {
            steps {
                git 'https://github.com/Aditya12155/my-app'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME:latest .'
            }
        }


        stage('Login to Docker Hub') {
        steps {
            script {
            withCredentials([string(credentialsId: 'dockerhub-token', variable: 'DOCKER_TOKEN')]) {
                sh '''
                echo $DOCKER_TOKEN | docker login -u adibhai --dckr_pat_n_MTIwRJEbSgjRbuZ_w-TqW7BI4
                '''
                }
            }
        }
    }
        

        stage('Push to Docker Hub') {
            steps {
                sh 'docker push $IMAGE_NAME:latest'
            }
        }
    }
}
