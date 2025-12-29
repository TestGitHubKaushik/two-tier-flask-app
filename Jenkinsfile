pipeline{
    agent { label 'worker1' }
    stages{
        stage("code clone"){
            steps{
                git url: "https://github.com/TestGitHubKaushik/two-tier-flask-app.git", branch: "master"
            }
        }
        stage('Build Docker Image') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'dockerHubCred',
                    usernameVariable: 'DOCKER_USER',
                    passwordVariable: 'DOCKER_PASS'
        )]) {

            sh '''
                echo "$DOCKER_PASS" | docker login -u "$DOCKER_USER" --password-stdin

                docker build -t two-tier-flask-app:latest .

                docker tag two-tier-flask-app:latest $DOCKER_USER/two-tier-flask-app:latest
                
                docker push $DOCKER_USER/two-tier-flask-app:latest
            '''
        }
    }
}
        stage("deploy using docker compose"){
            steps{
                sh "docker compose down"
                sh "docker compose up -d --build"
            }
        }
    }
}
