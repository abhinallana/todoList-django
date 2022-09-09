pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo 'This is the Checkout Stage'
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/abhinallana/todoList-django.git']]])
                echo 'docker --version'
            }
        }
        stage('Build'){
            steps{
                git branch: 'master', credentialsId: 'GithubCreds', url: 'https://github.com/abhinallana/todoList-django.git'
                sh 'sudo apt-get install docker'
                sh 'docker --version'
                sh 'docker build . -t todoDev'
            }
        }
        stage('Docker run and Publish'){
            steps{
                echo 'Build has completed, Running on Docker'
                sh 'sudo docker run -d -p 8000:8000 todo-dev'
            }
        }
        stage('End'){
            steps{
                echo 'The app is live on 127.0.0.1:8000'
            }
        }
    }
}
