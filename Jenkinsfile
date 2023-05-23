pipeline {
    agent any
    stages {
        stage("Clone Code") {
            steps {
                git url: "https://github.com/vishnureddy997/node-todo-cicd.git", branch: "master"
            }
        }
        stage("Build and Test") {
            steps {
                sh "docker build . -t node-app-test-new"
            }
        }
        stage("Push to Docker Hub") {
            environment {
                DOCKERHUB_CREDENTIALS = credentials('dockerHub')
            }
            steps {
                script {
                    docker.withRegistry('', DOCKERHUB_CREDENTIALS.username, DOCKERHUB_CREDENTIALS.password) {
                        sh "docker tag node-app-test-new ${DOCKERHUB_CREDENTIALS.username}/node-app-test-new:latest"
                        sh "docker push ${DOCKERHUB_CREDENTIALS.username}/node-app-test-new:latest"
                    }
                }
            }
        }
        stage("Deploy") {
            steps {
                sh "docker-compose down && docker-compose up -d"
            }
        }
    }
}
