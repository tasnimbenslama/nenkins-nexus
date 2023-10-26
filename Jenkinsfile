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
      
        stage("Publish to Nexus ") {
            steps {
                script {
                   def nexusArtifactUploader = NexusArtifactUploader.fromNexus3(192.168.1.3:8081,'NEXUS_CRED')
                    nexusArtifactUploader.publisher(repository: 'maven-central-repository', protocol: 'http', credentialsId: 'NEXUS_CRED', version: '1.0.SNAPSHOT', groupId: 'com.mycompany.app', artifactId: 'pom.my-app', packaging: 'jar', file: 'pom.xml')
                }
                    } else {
                        error "*** File: ${artifactPath}, could not be found";
                    }
                }
            }
        }
    }

