pipeline {
    agent any

    stages {
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t flask-jenkins-app .'
            }
        }

        stage('Run Docker Container') {
            steps {
                sh '''
                    docker stop flask-jenkins-container || true
                    docker rm flask-jenkins-container || true
                    docker run -d --name flask-jenkins-container -p 5000:5000 flask-jenkins-app
                '''
            }
        }

        stage('Test App') {
            steps {
                sh '''
                    sleep 5
                    curl -f http://localhost:5000 || exit 1
                '''
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}
