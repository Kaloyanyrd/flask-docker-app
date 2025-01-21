pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/Kaloyanyrd/flask-docker-app.git', credentialsID: 'bc988f7c-f9c5-446f-ab39-b7107025ad2b'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t flask-docker-app .'
            }
        }

        stage('Test') {
            steps {
                sh 'docker run -d --name flask-test -p 5000:5000 flask-docker-app'
                sh 'sleep 5'
                sh 'curl -f http://localhost:5000 || exit 1'
                sh 'docker stop flask-test && docker rm flask-test'
            }
        }

        stage('Deploy') {
            steps {
                sh 'docker run -d --name flask-app -p 5000:5000 flask-docker-app'
            }
        }
    }
}
