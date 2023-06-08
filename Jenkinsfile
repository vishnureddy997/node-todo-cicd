pipeline {
    agent any
    stages{
        stage("Clone Code"){
            steps{
                git url: "https://github.com/vishnureddy997/node-todo-cicd.git", branch: "master"
            }
        }
    
       stage('Build and Push Docker Image') {
      steps {
        script {
          def imageTag = "v1.0.${env.BUILD_NUMBER}" // Generate image tag using Jenkins build number
          def dockerImage = docker.build("dockerrepository123/testnodeapp:${imageTag}", ".")
          docker.withRegistry('https://index.docker.io/v1/', 'docker-cred') {
            dockerImage.push()
          }
          env.IMAGE_TAG = imageTag // Store the image tag in an environment variable for future 
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

