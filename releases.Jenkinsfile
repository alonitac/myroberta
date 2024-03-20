pipeline {
    agent any

    parameters { string(name: 'POLYBOT_PROD_IMG_URL', defaultValue: '', description: '') }

    stages {
        stage('Update YAML') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'github', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                    sh '''
                    git checkout releases
                    git merge origin/main
                    sed -i "s|image: .*|image: ${POLYBOT_PROD_IMG_URL}|g" k8s/prod/polybot.yaml
                    git add k8s/prod/polybot.yaml
                    git commit -m "$POLYBOT_PROD_IMG_URL"
                    git push https://alonitac:$PASSWORD@github.com/alonitac/myroberta.git releases
                    '''
                }
            }
        }
    }
}