pipeline {
    agent any 
    
    tools{
        maven 'mvn'
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
         stage("Build"){
            steps{
                sh " mvn clean install"
            }
        }
        
        stage("Docker Build"){
            steps{
                script{
                        sh "docker build -t image1 ."
                    }
                }
            }
    }
}
