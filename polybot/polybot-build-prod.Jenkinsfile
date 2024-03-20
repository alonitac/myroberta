pipeline {
    agent any

    environment {
        ECR_URL = "352708296901.dkr.ecr.eu-north-1.amazonaws.com"
    }

    stages {
        stage('Build') {
            steps {
                sh '''
                cd polybot
                aws ecr get-login-password --region eu-north-1 | docker login --username AWS --password-stdin $ECR_URL
                docker build -t $ECR_URL/alonit-polybot-prod:0.0.$BUILD_NUMBER .
                docker push $ECR_URL/alonit-polybot-prod:0.0.$BUILD_NUMBER
                '''
            }
        }

        stage('Trigger Release') {
            steps {
                build job: 'Release', wait: false, parameters: [
                    string(name: 'POLYBOT_PROD_IMG_URL', value: "${ECR_URL}/alonit-polybot-prod:0.0.${BUILD_NUMBER}")
                ]
            }
        }

    }
}