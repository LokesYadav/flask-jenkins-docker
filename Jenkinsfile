pipeline {
    agent any

    stages {
        stage('Clone') {
            steps {
                git 'https://github.com/LokesYadav/flask-jenkins-docker.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    docker.build('flask-jenkins-image')
                }
            }
        }

        stage('Run Docker Container') {
            steps {
                script {
                    docker.image('flask-jenkins-image').run('-p 5000:5000')
                }
            }
        }
    }
}
