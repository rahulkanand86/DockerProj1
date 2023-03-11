pipeline {
    agent any
    
    stages {
        stage('Build Docker Image') {
            steps {
                script {
                    docker.build('my-image-name:latest', '-f Dockerfile .')
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
