pipeline {
    agent any 
    
    environment {
        registry = "ak774/docker-test"
        registryCredential = 'dockerhub1'
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
            steps stage('login'){
            steps {
                bat 'docker login -u ak774 --password-stdin Salvere@881'
            }}
        
        stage('Push Image') {
            steps {
                bat 'docker push ak774/docker-test:%BUILD_NUMBER%'
            }
        }}

        post {
            always {
                bat 'docker logout'
                }
            }
        }
}
