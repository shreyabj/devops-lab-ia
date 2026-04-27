pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "bjshreya/myapp"
        TAG = "v1"
    }

    stages {

        stage('Clone Repo') {
            steps {
                git 'https://github.com/yourusername/repo.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t %DOCKER_IMAGE%:%TAG% .'
            }
        }

        stage('Login to Docker Hub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-creds', usernameVariable: 'USER', passwordVariable: 'PASS')]) {
                    bat 'echo %PASS% | docker login -u %USER% --password-stdin'
                }
            }
        }

        stage('Push Image') {
            steps {
                bat 'docker push %DOCKER_IMAGE%:%TAG%'
            }
        }
    }
}
