pipeline {
    agent any
    
    stages {
        stage('Declarative: Checkout SCM') {
            steps {
                checkout([$class: 'GitSCM', 
                          branches: [[name: '*/master']], 
                          doGenerateSubmoduleConfigurations: false, 
                          extensions: [], 
                          submoduleCfg: [], 
                          userRemoteConfigs: [[credentialsId: '65eeec4d-0e38-46aa-b240-12e4d39b3508', 
                                              url: 'https://github.com/Sivakrish241/jenkins_pipeline.git']]])
            }
        }
        
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
                script {
                    try {
                        sh 'docker stop my-node-app'
                    } catch (err) {
                        echo 'No container to stop'
                    }
                    try {
                        sh 'docker rm my-node-app'
                    } catch (err) {
                        echo 'No container to remove'
                    }
                }
            }
        }
        
        stage('Build Docker image') {
            steps {
                sh 'docker build -t my-node-app .'
            }
        }
        
        stage('Run Docker container') {
            steps {
                sh 'docker run -d --name my-node-app -p 3000:3000 my-node-app'
            }
        }
    }
}
