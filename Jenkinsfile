pipeline {
    agent any
    
    tools {
        maven 'mvn'
    }
    
    environment {
        SCANNER_HOME = tool 'sonar-scanner'
    }
    
    stages {
        stage("Compile") {
            steps {
                sh "mvn clean compile"
            }
        }
        
        stage("Test Cases") {
            steps {
                sh "mvn test"
            }
        }
        
        stage("Generate Code Coverage Report") {
            steps {
                sh "mvn jacoco:report"
            }
        }
        
        stage("Sonarqube Analysis") {
            steps {
                withSonarQubeEnv('SonarQube') {
                    withCredentials([string(credentialsId: 'sonarlatest', variable: 'SONAR_TOKEN')]) {
                        sh ''' $SCANNER_HOME/bin/sonar-scanner \
                        -Dsonar.projectName=cart \
                        -Dsonar.java.binaries=target/classes \
                        -Dsonar.projectKey=cart \
                        -Dsonar.sources=src/main/java \
                        -Dsonar.tests=src/test/java \
                        -Dsonar.test.inclusions=**/*Test.java \
                        -Dsonar.junit.reportPaths=target/surefire-reports \
                        -Dsonar.jacoco.reportPaths=target/site/jacoco/jacoco.xml \
                        -Dsonar.login=$SONAR_TOKEN '''
                    }
                }
            }
        }
        
        stage("Build") {
            steps {
                sh "mvn clean install"
            }
        }
    }
}
