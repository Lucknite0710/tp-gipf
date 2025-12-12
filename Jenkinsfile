pipeline {
    agent any

        stages {  
        stage('Build') {   
            steps {  
                sh 'mvn -B -DskipTests clean package'   
            }  
        } 
        stage('tester') {  
            steps {  
                sh 'mvn test'  
            }  
            post {  
                always {  
                    junit 'target/surefire-reports/*.xml'  
                }  
            }  
        }  
        stage('qualité de code') {  
            steps {  
                sh 'mvn clean package sonar:sonar'
            }  
        }
        stage('Déployer') {  
            steps {  
                sh './jenkins/scripts/deliver.sh'  
            }  
        }
                
    }
  }
