pipeline {
    agent {
        label "general"
        docker {
            image '352708296901.dkr.ecr.us-east-2.amazonaws.com/alonit-jenkins-agent:0.1'
            args  '--user root -v /var/run/docker.sock:/var/run/docker.sock'
        }
    }

    environment {
        ECR_URL = "700935310038.dkr.ecr.eu-north-1.amazonaws.com"

    }

    stages {
        stage('Build') {
            steps {
                sh '''
                pwd
                aws ecr get-login-password --region eu-north-1 | docker login --username AWS --password-stdin $ECR_URL
                docker build -t $ECR_URL/robberta:0.0.$BUILD_NUMBER .
                docker push $ECR_URL/robberta:0.0.$BUILD_NUMBER
                '''
            }
            post {
                always {
                    sh 'docker image prune -a --force'
                }
            }
        }

        stage('Trigger Deploy') {
            steps {
                build job: 'RobertaDeploy', wait: false, parameters: [
                    string(name: 'ROBERTA_IMAGE_URL', value: "${ECR_URL}/robberta:0.0.${BUILD_NUMBER}")
                ]
            }
        }
    }
}