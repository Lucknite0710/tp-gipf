pipeline {
  agent any
  environment {
    SONAR_TOKEN = credentials('sonar-token')
  }
  stages {
    stage('Checkout') {
      steps { checkout scm }
    }
    stage('Build') {
      steps {
        sh './gradlew clean build --no-daemon'
      }
    }
    stage('SonarQube Analysis') {
      steps {
        withSonarQubeEnv('sonar-token') {
          sh './gradlew sonarqube --no-daemon -Dsonar.login=$SONAR_TOKEN'
        }
      }
    }
    stage('Quality Gate') {
      steps {
        timeout(time: 1, unit: 'HOURS') {
          waitForQualityGate abortPipeline: true
        }
      }
    }
  }
  post {
    success {
      echo 'Build and SonarQube analyse avec succès.'
    }
    failure {
      echo 'Pipeline échoué.'
    }
  }
}
