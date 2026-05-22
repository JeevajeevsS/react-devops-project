pipeline {
    agent any

    environment {
        DOCKER_HUB_REPO = 'jeevas12/react-app'
    }

    stages {

        stage('Clone Code') {
            steps {
                git branch: 'main',
                url: 'https://github.com/JeevajeevsS/react-devops-project.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t ${DOCKER_HUB_REPO}:latest .'
            }
        }

        stage('Push to Docker Hub') {
            steps {

                withCredentials([usernamePassword(
                    credentialsId: 'dockerhub-creds',
                    usernameVariable: 'DOCKER_USER',
                    passwordVariable: 'DOCKER_PASS'
                )]) {

                    sh 'echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin'

                    sh 'docker push ${DOCKER_HUB_REPO}:latest'
                }
            }
        }
    }
}