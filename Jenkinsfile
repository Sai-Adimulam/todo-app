pipeline {
    agent any
       stages {
          stage ('Pull the code from github'){
            steps{
                git branch: 'main',url: 'https://github.com/Sai-Adimulam/todo-app.git'
            }
          }
          stage ('Build the Docker Image'){
            steps{
                bat 'docker build -t todo-app .'
            }
          }
          stage('Docker Hub Login') {
            steps {
                bat 'docker login -u adimulam22 -p Adimulam@2213'
            }
        }
          stage ('Push Image to Docker Hub'){
            steps{
                bat 'docker tag todo-app adimulam22/todo-app'
                bat 'docker push adimulam22/todo-app'
            }
          }
          stage('Create Ec2 instance'){
            steps{
                bat 'ssh -i F:\\keypairs\\todo-app-keypair.pem ubuntu@43.205.177.84 "docker pull adimulam22/todo-app"'
                bat 'ssh -i F:\\keypairs\\todo-app-keypair.pem ubuntu@43.205.177.84 "docker run -d -p 8083:80 adimulam22/todo-app"'
            }
          }
       }
}
