pipeline {
    agent { label 'jenkins-slave' }
    
    stages{
        stage('Code'){
            steps{
                git url: 'https://github.com/powersystems013/aws-node-todo-cicd.git', branch: 'master' 
            }
        }
        stage('Build and Test'){
            steps{
                sh 'docker build . -t kiet019/aws-node-todo-cicdK8s:latest'
            }
        }
        stage('Push'){
            steps{
                withCredentials([usernamePassword(credentialsId: 'dockerHub', passwordVariable: 'dockerHubPassword', usernameVariable: 'dockerHubUser')]) {
        	     sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPassword}"
                 sh 'docker push kiet019/aws-node-todo-cicdK8s:latest'
                }
            }
        }
        stage('Deploy'){
            steps{
                sh "docker-compose down && docker-compose up -d"
            }
        }
    }
}
