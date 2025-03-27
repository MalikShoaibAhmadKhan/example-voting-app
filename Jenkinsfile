pipeline {
    agent any

    triggers {
        genericTrigger(
            genericVariables: [
                [key: 'ref', value: '$.ref']
            ],
            token: 'github-webhook-token',  // Create this in Jenkins
            printContributedVariables: true,
            printPostContent: true
        )
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
