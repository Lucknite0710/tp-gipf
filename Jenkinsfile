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
        sh './gradlew --no-daemon -Dhttps.proxyHost=proxy1-rech -Dhttps.proxyPort=3128 clean build'
      }
    }
    stage('SonarQube Analysis') {
      steps {
        sh "./gradlew sonar -Dsonar.projectKey=TP_Controle -Dsonar.projectName=TP_Controle -Dsonar.host.url=http://localhost:9000 -Dsonar.login=$SONAR_TOKEN -Dhttps.proxyHost=proxy1-rech -Dhttps.proxyPort=3128 --no-daemon"
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
