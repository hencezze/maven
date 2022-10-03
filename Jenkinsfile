pipeline {
    agent any
    tools {
        maven "MAVEN"
    }
    
    environment {
          string_name = 'backend'
          version = 1.${random_num}
          max = 10
          random_num = "${Math.abs(new Random().nextInt(max+1))}"
    }
    
    stages {
        stage('Prepare Environment') {
            steps{
                buildName "${string_name}-${version}-${BUILD_TIMESTAMP}"
            }
        }
        
        stage('Build Maven') {
            steps{
                sh "mvn clean package"
                
            }
        }
    }
}
