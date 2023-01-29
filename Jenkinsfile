pipeline {
    agent any

    stages {
        stage('Build Docker Image') {
            steps {
                script {
                    dockerapp = docker.build("britotecst/kube-news:${env.BUILD_ID}", '-f ./src/Dockerfile ./src')
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', 'dockerhub')
                    def customImage = docker.build("britotecst/kube-news:${env.BUILD_ID}")
                    /* Push the container to the custom Registry */
                    customImage.push()
                }
            }
        }
    }
}