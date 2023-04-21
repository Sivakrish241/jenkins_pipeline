pipeline {
    agent any
    environment {
        DOCKER_IMAGE = "my-node-app"
    }
    stages {
        stage('Add Jenkins to Docker group') {
            steps {
                sh 'sudo adduser jenkins docker'
                sh 'sudo usermod -aG docker jenkins'
                sh 'sudo chown jenkins:jenkins /var/run/docker.sock'
                sh 'ls -l /var/run/docker.sock'
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
                sh 'docker build -t $DOCKER_IMAGE .'
            }
        }
        stage('Run Docker container') {
            steps {
                sh 'docker run -d -p 3000:3000 --name my-node-app $DOCKER_IMAGE'
            }
        }
    }
}
