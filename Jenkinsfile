pipeline {
    agent any

    environment {
        IMAGE_NAME = 'flask-jenkins-app'
        CONTAINER_NAME = 'flask-jenkins-container'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/LokesYadav/flask-jenkins-docker.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME .'
            }
        }

        stage('Run Docker Container') {
            steps {
                sh '''
                    docker rm -f $CONTAINER_NAME || true
                    docker run -d -p 5000:5000 --name $CONTAINER_NAME $IMAGE_NAME
                '''
            }
        }

        stage('Test App') {
            steps {
                sh 'sleep 3 && curl --fail http://localhost:5000 || echo "App test failed!"'
            }
        }
    }

    post {
        always {
            echo '✅ Pipeline completed!'
        }
        failure {
            echo '❌ Pipeline failed!'
        }
    }
}
