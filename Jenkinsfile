pipeline {
    agent any
    tools {
        maven "MAVEN"
    }
    
    stages {
        stage('Prepare Environment') {
            steps{
                buildName "backend-1.0-${BUILD_TIMESTAMP}"
            }
        }
        
        stage('Build Maven') {
            steps{
                sh "mvn clean package"
                
            }
        }
    }
}
