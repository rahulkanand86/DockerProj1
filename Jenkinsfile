pipeline {
    agent any
    
    stages {
        stage('Cleanup Docker') {
            steps {
                script {
                    // Stop and remove all running containers
                    docker.withServer('tcp://docker-host:2375') {
                        sh 'docker stop $(docker ps -aq)'
                        sh 'docker rm $(docker ps -aq)'
                    }

                    // Delete all Docker images
                    docker.withServer('tcp://docker-host:2375') {
                        sh 'docker rmi $(docker images -q)'
                    }
                }
            }
        stage('Build Docker Image') {
            steps {
                script {
                    def dockerfile = 'Dockerfile'
                    docker.build('my-image-name:latest', "-f ${dockerfile} .")
                }
            }
        }
        stage('Run Docker Container') {
            steps {
                script {
                    docker.image('my-image-name:latest').run('-p 80:80')
                }
            }
        }
    }
 }
}    
