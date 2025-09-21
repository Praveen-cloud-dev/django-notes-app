pipeline {
    agent any
    stages{
        stage("Clone Code"){
            steps{
                git url: "https://github.com/Praveen-cloud-dev/django-notes-app.git", branch: "dev"
            }
        }
        stage("Build and Test"){
            steps{
                sh "docker build . -t notes-app:latest"
            }
        }
        stage("Push to Docker Hub"){
            steps{
                withCredentials([usernamePassword(credentialsId:"dockerhubcred",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")]){
                sh "docker tag notes-app:latest $dockerHubUser}/notes-app:latest"
                sh "docker login -u $dockerHubUser -p $dockerHubPass"
                sh "docker push $dockerHubUser/notes-app:latestt"
                }
            }
        }
        stage("Deploy"){
            steps{
                sh "docker-compose down && docker-compose up -d"
            }
        }
    }
}
