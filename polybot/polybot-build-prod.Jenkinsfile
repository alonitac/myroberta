pipeline {
    agent any

    environment {
        ECR_URL = "700935310038.dkr.ecr.eu-north-1.amazonaws.com"
    }

    stages {
        stage('Build') {
            steps {
                sh '''
                cd polybot
                aws ecr get-login-password --region eu-north-1 | docker login --username AWS --password-stdin $ECR_URL
                docker build -t $ECR_URL/polybot:0.0.$BUILD_NUMBER .
                docker push $ECR_URL/polybot:0.0.$BUILD_NUMBER
                '''
            }
        }
    }
}