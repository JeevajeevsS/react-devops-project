pipeline {
    agent any

    environment {
        DOCKER_HUB_REPO = 'jeevas12/react-app'
        APP_SERVER = '65.0.129.131'
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
                    credentialsId: 'jeevas12',
                    usernameVariable: 'DOCKER_USER',
                    passwordVariable: 'DOCKER_PASS'
                )]) {

                    sh 'echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin'

                    sh 'docker push ${DOCKER_HUB_REPO}:latest'
                }
            }
        }

        stage('Deploy To EC2') {
            steps {
                sh """
                ssh -o StrictHostKeyChecking=no -i /var/lib/jenkins/app.pem ec2-user@${APP_SERVER} << 'EOF'

                sudo docker stop react-app || true
                sudo docker rm react-app || true

                sudo docker pull ${DOCKER_HUB_REPO}:latest

                sudo docker run -d -p 80:3000 --name react-app ${DOCKER_HUB_REPO}:latest

                EOF
                """
            }
        }
    }
}