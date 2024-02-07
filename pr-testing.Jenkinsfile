pipeline {
    agent any

    stages {
        stage('Unittest') {
            steps {
                sh 'exit 1'
            }
        }
        stage('Lint') {
            steps {
                sh 'echo "linting"'
            }
        }
        stage('Functional test') {
            steps {
                sh 'echo "testing"'
            }
        }
    }
}