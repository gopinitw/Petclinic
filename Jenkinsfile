pipeline {
    agent any 
    
    environment {
        SONAR_ENV = 'sonarqube-local'
    }
    
    stages{
        
            stage('Build + Test + Sonar') {
            steps {
                withSonarQubeEnv("${SONAR_ENV}") {
                    sh '''
                      mvn clean verify sonar:sonar \
                      -Dsonar.projectKey=java-demo \
                      -Dsonar.projectName="Java Demo App"
                    '''
                }
            }
        }
        
    }
}
