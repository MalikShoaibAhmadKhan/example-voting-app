pipeline {
    agent any

    triggers {
        githubPush()  // ✅ Correct GitHub webhook trigger
    }

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', 
                    url: 'https://github.com/MalikShoaibAhmadKhan/example-voting-app.git',
                    credentialsId: 'github-token'
            }
        }

        stage('Build and Restart Containers') {
            steps {
                sh '''
                docker-compose down
                docker-compose up -d --build
                '''
            }
        }

        stage('Verify Deployment') {
            steps {
                sh 'docker ps'
            }
        }
    }
}
