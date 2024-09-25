pipeline {
    agent any 
    
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
                bat 'docker build -t ak774/node_app:%BUILD_NUMBER% .'
            }
        }
        stage('Login to Docker Hub') {
            steps {
               withCredentials([string(credentialsId: 'test-dockerhub-password', variable: 'test-dockerhub-password')]) {
                    script {
                        bat 'docker login -u ak774 -p ${test-dockerhub-password}'
                    }
                }
            }
        }
        stage('Push Image') {
            steps {
                bat 'docker push ak774/node_app:%BUILD_NUMBER%'
            }
        }
    }
    post {
        always {
            bat 'docker logout'
        }
    }
}
