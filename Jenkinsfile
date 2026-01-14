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
            mvn -B clean verify org.sonarsource.scanner.maven:sonar-maven-plugin:sonar \
              -Dsonar.host.url=http://localhost:9000 \
              -Dsonar.login=$SONAR_TOKEN \
              -Dsonar.projectKey=student-management
          '''
        }
      }
    }
  }
}

