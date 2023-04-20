pipeline {
    agent any
    
    stages {
        stage('Add Jenkins to Docker group') {
            steps {
                sh 'sudo usermod -aG docker jenkins'
            }
        }
        
        stage('Restart Docker') {
            steps {
                sh 'sudo systemctl restart docker'
            }
        }
        
        stage('Change Docker socket permissions') {
            steps {
                sh 'sudo chgrp docker /var/run/docker.sock'
            }
        }
        
        stage('Stop and remove existing container') {
            steps {
                sh 'docker stop my-node-app || true'
                sh 'docker rm my-node-app || true'
            }
        }
        
        stage('Build Docker image') {
            steps {
                sh 'docker build -t my-node-app .'
            }
        }
        
        stage('Run Docker container') {
            steps {
                sh 'docker run -d --name my-node-app -P 3000:3000 my-node-app'
            }
        }
    }
}
