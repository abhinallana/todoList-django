pipeline {
  agent any
    
  stages {

    stage('CheckOut') {
      steps {
        checkout([$class: 'GitSCM', branches: [[name: '*/develop']], extensions: [], userRemoteConfigs: [[credentialsId: 'GithubCreds', url: 'https://github.com/abhinallana/
todoList-django.git']]])
      }
    }
     
    stage('Build') {
      steps {
        git branch: 'develop', credentialsId: 'GithubCreds', url: 'https://github.com/abhinallana/todoList-django.git'
        sh 'docker build . -t todoDev'
      }
    } 
    stage('Push and run Docker') {
      steps {
          sh "docker run -d -p 8000:8000 todoDev"
          } 

    }
    
    stage('Deploy') {
      steps {
         echo 'Check live App on http://127.0.0.1:8000/todos'
         sh 'python manage.py runserver' // http://127.0.0.1:8000/todos to check the running app
      }
    }  
  }
}