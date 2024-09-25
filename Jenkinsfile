pipeline {
    agent any 
    
    environment {
        registry = "ak774/docker-test"
        registryCredential = 'dockerhub'
        dockerImage = ' '
    }
    
    stages { 
        stage('SCM Checkout') {
            steps {
                retry(3) {
                    git branch: 'main', url: 'https://github.com/Ak9994/Demo'
                }
            }
        }
        stage('Build Docker Image') {
            steps {  
                bat 'docker build -t ak774/docker-test:%BUILD_NUMBER% .'
            }
        }
        stage('Login to Docker Hub') {
            steps {
               docker.withRegistry([string(credentialsId: 'DockerPwd',variable:'dockerpwd')]){
                   script{ bat 'docker login -u ak774 -p {dockerpwd}' }
            }
        }
        stage('Push Image') {
            steps {
                bat 'docker push ak774/docker-test:%BUILD_NUMBER%'
            }
        }
    }
    post {
        always {
            echo 'status'
            bat 'docker logout'
        }
    }
}}
