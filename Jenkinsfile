pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "hemanth2006kb/imagename5"
        IMAGE_TAG = "latest"
    }

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'master',
                    url: 'https://github.com/Hemanthkb2006/prac.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat "docker build -t %DOCKER_IMAGE%:%IMAGE_TAG% ."
            }
        }

        stage('Login to Docker Hub') {
            steps {
                withCredentials([string(
                    credentialsId: 'dockerhub-PAT',
                    variable: 'DOCKER_PAT'
                )]) {
                    bat 'echo %DOCKER_PAT%| docker login -u hemanth2006kb --password-stdin'
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                bat "docker push %DOCKER_IMAGE%:%IMAGE_TAG%"
            }
        }
    }

    post {
        success {
            echo 'Docker image built and pushed successfully.'
        }
        failure {
            echo 'Pipeline failed. Check Console Output.'
        }
    }
}
