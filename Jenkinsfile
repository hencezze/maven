pipeline {
    agent any
    tools {
        maven "MAVEN"
    }
    
    environment {
          string_name = 'backend'
          max = 10
          rand = "${Math.abs(new Random().nextInt(max+1))}"
    }
    
    stages {
        stage('Prepare Environment') {
            steps{
                buildName "${string_name}-1.${rand}-${BUILD_TIMESTAMP}"
            }
        }
        
        stage('Build Maven') {
            steps{
                sh "mvn clean package"
            }
        }
    }
}
