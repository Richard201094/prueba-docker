pipeline {
    agent any
    environment {
        DockerUsername = 'richardtorres'
        GithubUsername = 'richard201094/prueba-docker'
        DockerName = 'imagenprueba'
        DockerTag = 'latest'
        DockerLoginCredentials = 'f24dbf03-9e78-40ff-b23b-2522e4eaccf1'
        GithubLoginCredentials = '163527aa-bc0d-4ac6-a48f-3a0f7befc084'
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
                        def image = docker.build("${DockerUsername}/${DockerName}:${DockerTag}")
                        image.push()
                    }
                    // Github registry
                    docker.withRegistry('https://docker.pkg.github.com', GithubLoginCredentials) {
                        def image = docker.build("${GithubUsername}/${DockerName}:${DockerTag}")
                        image.push()
                    }
                }
            }
        }
    }
}