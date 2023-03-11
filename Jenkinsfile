pipeline {
    agent any
    
    stages {
        stage('Cleanup Docker') {
            steps {
                script {
                    // Stop and remove all running containers
                    docker.withServer('tcp://localhost:80') {
                        sh 'docker stop $$(docker ps -aq)'
                        sh 'docker rm $$(docker ps -aq)'
                    }

                    // Delete all Docker images
                    docker.withServer('tcp://localhost:80') {
                        sh 'docker rmi $$(docker images -q)'
                    }
                }
            }
        }
        
        // Add other stages here to build and run Docker containers
        // ...
        stage('Build Docker Image') {
            steps {
                script {
                    def dockerfile = 'Dockerfile.dev'
                    docker.build('my-image-name:latest', "-f ${dockerfile} .")
                }
            }
        }
        stage('Run Docker Container') {
            steps {
                script {
                    docker.image('my-image-name:latest').run('-p 8080:80')
                }
            }
        }
    }
}
