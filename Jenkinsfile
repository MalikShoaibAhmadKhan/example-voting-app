pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', 
                    url: 'https://github.com/MalikShoaibAhmadKhan/example-voting-app.git', 
                    credentialsId: 'github-token'  // Ensure this matches the credential ID in Jenkins
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t your-image-name .'
            }
        }

        stage('Run Container') {
            steps {
                sh 'docker run -d -p 5000:5000 your-image-name'
            }
        }
    }
}
