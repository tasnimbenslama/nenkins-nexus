pipeline {
    agent any
    tools {
        maven "M2_HOME"
    }
    environment {
        NEXUS_VERSION = "nexus3"
        NEXUS_PROTOCOL = "http"
        NEXUS_REPOSITORY = "java-app"
        NEXUS_URL = "192.168.1.3:8081"
      
        NEXUS_CREDENTIAL_ID = "NEXUS_CRED"
    }
    stages {
        stage("Clone code from GitHub") {
            steps {
                script {
                    git branch: 'main', url: 'https://github.com/tasnimbenslama/nenkins-nexus.git';
                }
            }
        }
        stage("Maven Build") {
            steps {
                script {
                    sh "mvn package -DskipTests=true"
                }
            }
        }
      
        stage("Publish to Nexus Repository Manager") {
            steps {
                script {
                   
                    if(artifactExists) {
                        echo "*** File: ${artifactPath}, group: ${pom.groupId}, packaging: ${pom.packaging}, version ${pom.version}";
                        nexusArtifactUploader(
                            nexusVersion: 'nexus3',
                            protocol: 'http',
                            nexusUrl: '192.168.1.3:8081',
                            groupId: 'pom.com.mycompany.app',
                            version: 'pom.1.0.SNAPSHOT',
                            repository: 'maven-central-repository',
                            credentialsId: 'NEXUS_CRED',
                            artifacts: [
                                [artifactId: 'pom.my-app',
                                classifier: '',
                                file: artifactPath,
                                type: pom.packaging],
                                [artifactId: 'pom.my-app',
                                classifier: '',
                                file: "pom.xml",
                                type: "pom"]
                            ]
                        );
                    } else {
                        error "*** File: ${artifactPath}, could not be found";
                    }
                }
            }
        }
    }
}
