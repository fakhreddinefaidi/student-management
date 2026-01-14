pipeline {
  agent any

  stages {

    stage('Clean workspace') {
      steps {
        // Nettoyage pour éviter que Jenkins garde un ancien build
        deleteDir()
      }
    }

    stage('Checkout') {
      steps {
        git branch: 'main', url: 'https://github.com/fakhreddinefaidi/student-management.git'
      }
    }

    stage('Debug (commit + pom)') {
      steps {
        sh '''
          echo "=== GIT INFO ==="
          git rev-parse HEAD || true
          git branch -a || true

          echo "=== CHECK JPA IN POM ==="
          ls -la
          echo "--- pom.xml (search spring-boot-starter-data-jpa) ---"
          grep -n "spring-boot-starter-data-jpa" pom.xml || echo "NOT FOUND: spring-boot-starter-data-jpa"
        '''
      }
    }

    stage('Build + Sonar') {
      steps {
        withCredentials([string(credentialsId: 'sonar-token', variable: 'SONAR_TOKEN')]) {
          sh '''
            mvn -B clean verify org.sonarsource.scanner.maven:sonar-maven-plugin:3.11.0.3922:sonar \
              -Dsonar.host.url=http://localhost:9000 \
              -Dsonar.token=$SONAR_TOKEN \
              -Dsonar.projectKey=student-management
          '''
        }
      }
    }
  }
}

