pipeline {
    agent any
    environment {
        DOCKER_IMAGE_VOTE = "malikshoaib/vote-app"
        DOCKER_IMAGE_RESULT = "malikshoaib/result-app"
        DOCKER_IMAGE_WORKER = "malikshoaib/worker-app"
    }
    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/MalikShoaibAhmadKhan/example-voting-app.git'
            }
        }
        stage('Build Docker Images') {
            steps {
                sh 'docker build -t $DOCKER_IMAGE_VOTE ./vote'
                sh 'docker build -t $DOCKER_IMAGE_RESULT ./result'
                sh 'docker build -t $DOCKER_IMAGE_WORKER ./worker'
            }
        }
        stage('Push to Docker Hub') {
            steps {
                withCredentials([string(credentialsId: 'docker-hub-credentials', variable: 'DOCKER_HUB_PASS')]) {
                    sh 'echo $DOCKER_HUB_PASS | docker login -u malikshoaib --password-stdin'
                    sh 'docker push $DOCKER_IMAGE_VOTE'
                    sh 'docker push $DOCKER_IMAGE_RESULT'
                    sh 'docker push $DOCKER_IMAGE_WORKER'
                }
            }
        }
        stage('Deploy Application') {
            steps {
                sh 'docker-compose down'
                sh 'docker-compose up -d'
            }
        }
    }
}
