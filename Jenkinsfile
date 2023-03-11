pipeline {
    agent any
    
    stages {
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
