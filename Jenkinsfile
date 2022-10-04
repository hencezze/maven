pipeline {
    agent any
    parameters {
     booleanParam name: 'runTEST'   
     }
    tools {
        maven "MAVEN"
    }
    
    environment {
          string_name = 'backend'
          max = 10
          rand = "${Math.abs(new Random().nextInt(max+1))}"
          NEXUS_VERSION = "nexus3"
          NEXUS_PROTOCOL = "http"
          NEXUS_URL = "172.19.0.3:8081"
          NEXUS_REPOSITORY = "nexus"
          NEXUS_CREDENTIAL_ID = "jenk"
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
        stage("Publish to Nexus Repository Manager") {
            steps {
                script {
                    pom = readMavenPom file: "pom.xml";
                    filesByGlob = findFiles(glob: "target/*.${pom.packaging}");
                    echo "${filesByGlob[0].name} ${filesByGlob[0].path} ${filesByGlob[0].directory} ${filesByGlob[0].length} ${filesByGlob[0].lastModified}"
                    artifactPath = filesByGlob[0].path;
                    artifactExists = fileExists artifactPath;
                    if(artifactExists) {
                        echo "*** File: ${artifactPath}, group: ${pom.groupId}, packaging: ${pom.packaging}, version ${pom.version}";
                        nexusArtifactUploader(
                            nexusVersion: NEXUS_VERSION,
                            protocol: NEXUS_PROTOCOL,
                            nexusUrl: NEXUS_URL,
                            groupId: pom.groupId,
                            version: pom.version,
                            repository: NEXUS_REPOSITORY,
                            credentialsId: NEXUS_CREDENTIAL_ID,
                            artifacts: [
                                [artifactId: pom.artifactId,
                                classifier: '',
                                file: artifactPath,
                                type: pom.packaging],
                                [artifactId: pom.artifactId,
                                classifier: '',
                                file: "pom.xml",
                                type: "pom"]
                            ]
                        );
                }   }
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
