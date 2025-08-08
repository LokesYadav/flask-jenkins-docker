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
            sh "docker rm -f ${CONTAINER_NAME} || true"
            docker.image("${IMAGE_NAME}").run("-d --name ${CONTAINER_NAME} -p 5000:5000")
        }
    }
}

    }
}
