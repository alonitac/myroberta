pipeline {
    agent any

    environment {
        ECR_URL = "352708296901.dkr.ecr.eu-north-1.amazonaws.com"
    }

    stages {
        stage('Build') {
            steps {
                sh '''
                cd yolo5
                aws ecr get-login-password --region eu-north-1 | docker login --username AWS --password-stdin $ECR_URL
                docker build -t $ECR_URL/alonit-yolo5-prod:0.0.$BUILD_NUMBER .
                docker push $ECR_URL/alonit-yolo5-prod:0.0.$BUILD_NUMBER
                '''
            }
        }

        stage('Trigger Release') {
            steps {
                build job: 'Release', wait: false, parameters: [
                    string(name: 'IMG_URL', value: "${ECR_URL}/alonit-yolo5-prod:0.0.${BUILD_NUMBER}")
                ]
            }
        }

    }
}