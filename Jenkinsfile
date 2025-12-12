pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building...'
            }
        }
        stage('Test') {
            steps {
                stage('SonarQube analysis') {
                    withSonarQubeEnv() { // Will pick the global server connection you have configured
                        sh './gradlew sonar'
                    }
                }
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}
