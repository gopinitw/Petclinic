pipeline {
    agent any 
    
    environment {
        SONAR_ENV = 'sonarqube-local'
    }
    
    stages{
        
        stage("Compile"){
            steps{
                sh "mvn clean compile"
            }
        }
        
         stage("Test Cases"){
            steps{
                sh "mvn test"
            }
        }
        
        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv("${SONAR_ENV}") {
                    sh '''
                      mvn sonar:sonar \
                      -Dsonar.projectKey=java-demo \
                      -Dsonar.projectName="Java Demo App"
                    '''
                }
            }
        }
        
    }
}
