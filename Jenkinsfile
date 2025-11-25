pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                git 'https://github.com/fakhreddinefaidi/student-management.git'
            }
        }

        stage('Build Maven') {
            steps {
                sh 'mvn clean package -DskipTests'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t fakhreddinefaidi/student-management:latest .'
            }
        }

        stage('Docker Login') {
            steps {
                sh 'echo $DOCKER_PASSWORD | docker login -u $DOCKER_USERNAME --password-stdin'
            }
        }

        stage('Push Image') {
            steps {
                sh 'docker push fakhreddinefaidi/student-management:latest'
            }
        }
    }
}
