pipeline {
    agent any

    stages {
        stage('Clone Repo') {
            steps {
                git 'https://github.com/LokesYadav/flask-jenkins-docker.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("flask-jenkins-app")
                }
            }
        }

        stage('Run Docker Container') {
            steps {
                script {
                    // Stop existing container if any
                    sh 'docker stop flask-jenkins-container || true'
                    sh 'docker rm flask-jenkins-container || true'

                    // Run the new container
                    sh 'docker run -d --name flask-jenkins-container -p 5000:5000 flask-jenkins-app'
                }
            }
        }

        stage('Test App') {
            steps {
                script {
                    sleep(time: 5, unit: "SECONDS") // wait for app to start
                    sh 'curl -f http://localhost:5000 || exit 1'
                }
            }
        }
    }

    post {
        failure {
            echo 'Pipeline failed!'
        }
        success {
            echo 'Pipeline completed successfully!'
        }
    }
}
