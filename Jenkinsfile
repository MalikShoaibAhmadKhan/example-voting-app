pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/MalikShoaibAhmadKhan/example-voting-app.git'
            }
        }

        stage('Build and Start Containers') {
            steps {
                sh 'docker-compose up -d --build'
            }
        }

        stage('Verify Running Containers') {
            steps {
                sh 'docker ps'
            }
        }
    }
}
