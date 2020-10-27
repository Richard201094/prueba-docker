pipeline {
    agent any
    environment {
        DockerUsername = 'richardtorres'
        GithubUsername = 'richard201094/prueba-docker'
        DockerName = 'imagenprueba'
        DockerTag = 'latest'
        DockerLoginCredentials = 'f24dbf03-9e78-40ff-b23b-2522e4eaccf1'
        GithubLoginCredentials = 'af5d1559-94a6-4420-af6b-2e3024d6f7ea'
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
				sh 'ls -la'
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
	post {
        always {
            sh 'ls -la' /* ver el contenido de la carpeta*/
            sh 'docker images' /* listar las imagenes*/
            sh "docker images | grep ${DockerName} | awk '{print \$3}' | xargs docker rmi -f" /* borramos todas las imagenes*/
            deleteDir() /* clean up our workspace */
            sh 'ls -la' /* ver el contenido de la carpeta*/
            sh 'docker images' /* listar las imagenes*/
        }
        success {
            echo 'OK'
        }
        failure {
            echo 'KO'
        }
    }
}