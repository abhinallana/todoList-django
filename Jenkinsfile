node{
        stage('Checkout') {
                echo 'This is the Checkout Stage'
                git 'https://github.com/abhinallana/todoList-django.git'
            }
        
        stage('Docker build'){
                sh 'docker --version'
                sh 'docker build . -t abhinallana/tododjango:v2'
            }
        
        stage('Docker Login') {
                withCredentials([string(credentialsId: 'dockerpwd', variable: 'dockerpwd')]) {
                 sh 'docker login -u abhinallana -p ${dockerpwd}'
                 echo "Successfully Logged into Docker"
                }
            }
        stage('Docker Push'){
                echo 'Build has completed, Pushing to DockerHub'
                sh 'docker push abhinallana/tododjango:v2'
            }
        stage('End'){
                def buildNo = "${BUILD_NUMBER}"
                echo 'Succesfully Built the Job in ${buildNo}th time. '
            }
    }

