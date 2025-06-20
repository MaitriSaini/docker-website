pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'yourdockerhubusername/barista-cafe'
        DOCKER_CREDENTIALS_ID = 'dockerhub-creds-id'  // Set this in Jenkins Credentials
    }

    stages {
        stage('Clone Repo') {
            steps {
                git 'https://github.com/Maitrisaaini/docker-website.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("${DOCKER_IMAGE}")
                }
            }
        }

        stage('Run Docker Container') {
            steps {
                sh 'docker run -d -p 887:80 ${DOCKER_IMAGE}'
            }
        }

        stage('Push to DockerHub') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', "${DOCKER_CREDENTIALS_ID}") {
                        docker.image("${DOCKER_IMAGE}").push('latest')
                    }
                }
            }
        }
    }
}
