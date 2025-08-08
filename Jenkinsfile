pipeline {
    agent any

    stages {
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
                    // Stop and remove previous container if exists
                    sh 'docker stop flask-jenkins-container || true'
                    sh 'docker rm flask-jenkins-container || true'

                    // Run new container
                    sh 'docker run -d --name flask-jenkins-container -p 5000:5000 flask-jenkins-app'
                }
            }
        }

        stage('Test App') {
            steps {
                script {
                    sleep(time: 5, unit: "SECONDS") // Give time to boot
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
