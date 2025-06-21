pipeline {
    agent any

    stages {
        stage('Clone Repo') {
            steps {
                git url: 'https://github.com/MaitriSaini/docker-website.git', branch: 'main'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t barista-app .'
            }
        }

        stage('Run Docker Container') {
            steps {
                sh 'docker run -d -p 358:80 barista-app'
            }
        }

        stage('Push to DockerHub') {
    steps {
        withCredentials([usernamePassword(credentialsId: '57ac0801-17b3-46d6-bd3e-297340019450', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
            sh """
                docker login -u $DOCKER_USER -p $DOCKER_PASS
                docker tag barista-app maitrisaini18/barista-app 
                docker push maitrisaini18/barista-app  
            """
                }
            }
        }
    }
}

