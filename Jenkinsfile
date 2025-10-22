@Library("Shareable") _
pipeline {
    agent {
        label 'aadil-agent'
    }
    
    stages {
        stage("Hello"){ 
        steps{
            script{
                hello()
            }
        }
    }
        stage('Code') {
            steps {
                script{
                    clone("https://github.com/ShaikhAadil010/django-notes-app.git", "main")
                }
            }
        }
        stage('Build') {
            steps {
               script{
                   docker_build("notes-app", "latest", "aadil010")
               }
            }
        }
        stage('Push to DockerHub'){
            steps{
              script{
                  docker_push("notes-app", "latest", "aadil010")
              }   
          }
        }
        stage('Deploy'){
            steps{
                echo 'Code deploying process start'
                sh 'docker compose down && compose up -d'
            }
        }
    }
}
