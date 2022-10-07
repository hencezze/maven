pipeline {
    agent { label 'dev' }
    parameters {
     booleanParam name: 'runTEST'   
     }
    
    environment {
          string_name = 'backend'
          max = 10
          rand = "${Math.abs(new Random().nextInt(max+1))}"
     }
    
    stages {
        stage('Prepare Job Name') {
            steps{
                buildName "${string_name}-1.${rand}-${BUILD_TIMESTAMP}"
            }
        }
        
        stage('Add git repo') {
            steps{
                git branch: 'main', credentialsId: 'inn', url: 'https://gitlab-trainee.inno.ws/jenkins-moodle-course/maven-simple-project.git'
            }
        }
        
        stage('Build Maven') {
            steps{
                sh "mvn clean package"
            }
        }
        stage('To nexus') {
            steps{
                sh "mvn deploy:deploy-file -DgroupId=innowise-group -DartifactId=henceze-app -Dversion=1.0 -Dpackaging=jar -Dfile=/workspace/backend/target/my-app-1.0-SNAPSHOT.jar -DgeneratePom=true -DrepositoryId=maven  -Durl=http://172.21.0.4:8081/repository/maven/"
            }
        }
        
        stage('Delete Artifact') {
            steps{
                sh "rm -Rfv /workspace/backend/*"
            }
        }
        
        stage('RunTest?') {
            steps {
                script {
                    if (runTEST == 'true') {
                        build job: 'test'
                    } else {
                        echo 'Boolean value is false'
                    }
                }
            }
        }
    }
}
