pipeline {
    agent {
        
    }
    stages {
        stage('build && SonarQube analysis') {
            steps {
                withSonarQubeEnv('sonar.tools.****) {
                 script {
                     cmd.withNexusCredentials {
                            sh 'gradle --info sonarqube  -Dsonar.projectKey=catalog-service -Dsonar.junit.reportPaths=./build/test-results/test -Dsonar.binaries=./build/classes -Dsonar.coverage.jacoco.xmlReportPaths=./build/reports/jacoco/test/html/index.html'
                        }
                }
            }
        }
    }
        stage("Quality Gate") {
            steps {
                timeout(time: 1, unit: 'HOURS') {
                    // Parameter indicates whether to set pipeline to UNSTABLE if Quality Gate fails
                    // true = set pipeline to UNSTABLE, false = don't
                    // Requires SonarScanner for Jenkins 2.7+
                    waitForQualityGate abortPipeline: true
                }
            }
        }
    }
}
