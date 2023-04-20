pipeline {
    agent any

    stages {
        stage('Stop Container') {
            steps {
                sh 'docker stop my-node-app || true' // the `|| true` prevents the build from failing if the container is not running
            }
        }
        stage('Remove Container') {
            steps {
                sh 'docker rm my-node-app || true'
            }
        }
        stage('Build Image') {
            steps {
                sh 'docker build -t my-node-app .'
            }
        }
        stage('Start Container') {
            steps {
                sh 'docker run -d --name my-node-app -p 3000:3000 my-node-app'
            }
        }
    }
}

