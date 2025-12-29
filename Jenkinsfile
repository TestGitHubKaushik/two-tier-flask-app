pipeline{
    agent { label 'worker1' }
    stages{
        stage("code clone"){
            steps{
                git url: "https://github.com/TestGitHubKaushik/two-tier-flask-app.git", branch: "master"
            }
        }
        stage("build docker image"){
            steps{
                sh "docker build -t two-tier-flask-app:latest ."
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
