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
               post {
                always {
                    // Publish JUnit results
                    junit 'target/surefire-reports/*.xml'
                    // Publish JaCoCo coverage
                    jacoco execPattern: 'target/jacoco.exec'
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
