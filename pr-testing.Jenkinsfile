pipeline {
    agent any

    stages {
        stage('Install requirements'){
            steps {
                sh 'pip install pytest pylint'
            }
        }
        stage('Unittest') {
            steps {
                sh '''
                python3 -m pytest --junitxml results.xml tests
                '''
            }
            post {
                always {
                    junit allowEmptyResults: true, testResults: 'results.xml'
                }
            }
        }

        stage('Lint') {
            steps {
                sh 'python3 -m pylint *.py'
            }
        }
        stage('Functional test') {
            steps {
                sh 'echo "testing"'
            }
        }
    }
}