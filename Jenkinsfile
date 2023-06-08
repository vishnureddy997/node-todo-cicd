pipeline {
    agent any
    stages{
        stage("Clone Code"){
            steps{
                git url: "https://github.com/vishnureddy997/node-todo-cicd.git", branch: "master"
            }
        }
        stage("Push to Docker Hub"){
            steps{
                def imageTag = "v1.0.${env.BUILD_NUMBER}"
                def dockerImage = docker.build("dockerrepository123/testnodeapp:${imageTag}", ".")
                docker.withRegistry('https://index.docker.io/v1/', 'dockerHub') {
                 dockerImage.push()
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
