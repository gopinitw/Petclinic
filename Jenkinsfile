pipeline {
    agent any
    
    tools {
        maven 'mvn' // Reference the Maven tool configured in Jenkins
    }
    
    environment {
        SCANNER_HOME = tool 'sonar-scanner' // Reference the SonarQube Scanner tool configured in Jenkins
    }
    
    stages {
        stage("Compile") {
            steps {
                sh "mvn clean compile" // Compile the project
            }
        }
        
        stage("Test Cases") {
            steps {
                sh "mvn test" // Run test cases
            }
        }
        
        stage("Sonarqube Analysis") {
            steps {
                withSonarQubeEnv('SonarQube') { // Use the SonarQube server configuration
                    withCredentials([string(credentialsId: 'sonar-token', variable: 'SONAR_TOKEN')]) { // Use the SonarQube token from Jenkins credentials
                        sh ''' $SCANNER_HOME/bin/sonar-scanner -Dsonar.projectName=Petclinic \
                        -Dsonar.java.binaries=. \
                        -Dsonar.projectKey=Petclinic \
                        -Dsonar.login=$SONAR_TOKEN ''' // Run the SonarQube scanner
                    }
                }
            }
        }
        
        stage("Build") {
            steps {
                sh "mvn clean install" // Build the project
            }
        }
    }
}
