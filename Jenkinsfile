pipeline {
    agent any
    environment {
        DockerUsername = 'sasarafalsky'
        DockerName = 'prueba-c2'
        DockerTag = '$BUILD_NUMBER'
        DockerLoginCredentials = 'f24dbf03-9e78-40ff-b23b-2522e4eaccf1'
    }
    stages {
        stage ('¿Quien soy 😀?') {
            steps {
                sh 'whoami'
            }
        }
        stage ('¿Donde 👌 estoy?') {
            steps {
                sh 'pwd'
            }
        }
        stage ('Docker images') {
            steps {
                sh 'docker images'
            }
        }
        stage ('Docker build') {
            steps {
                script {
                    // Docker Hub
                    docker.withRegistry('', DockerLoginCredentials) {
                        def image = docker.build("${DockerUsername}/${DockerName}:0.${DockerTag}")
                        image.push()
                    }
                }
            }
        }
    }
}