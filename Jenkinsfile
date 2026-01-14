pipeline {
  agent any

  stages {
    stage('Checkout') {
      steps {
        git branch: 'main', url: 'https://github.com/fakhreddinefaidi/student-management.git'
      }
    }

    stage('Build + Sonar') {
      steps {
        withCredentials([string(credentialsId: 'sonar-token', variable: 'SONAR_TOKEN')]) {
          sh '''
            mvn -B clean verify \
              org.sonarsource.scanner.maven:sonar-maven-plugin:3.11.0.3922:sonar \
              -Dsonar.host.url=http://localhost:9000 \
              -Dsonar.token=$SONAR_TOKEN \
              -Dsonar.projectKey=student-management
          '''
        }
      }
    }
  }
}

