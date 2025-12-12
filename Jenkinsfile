pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building..'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
        stage('Sonarqube'){
            steps {
                mvn clean verify sonar:sonar 
                  -Dsonar.projectKey=TP_Controle 
                  -Dsonar.projectName='TP_Controle 
                  -Dsonar.host.url=http://localhost:9000
                    -Dsonar.token=sqp_5f1c14a4139a5cbb0f7ceb65aab92d71f6d318f8
            }
        }
                
        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('SonarQube') {
                  sh 'npm run sonar'
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
    failure {
      echo 'Qualité non atteinte – pipeline aborted.'
    }
  }
}
