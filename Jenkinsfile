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
       stage('Publish to Nexus') {
            steps {
                script {
                    def nexusUrl = 'http://192.168.1.3:8081' // Remplacez par l'URL de votre Nexus
                    def nexusRepository = 'maven-central-repository' // Remplacez par le nom de votre repository Nexus
                    def nexusCredentialId = 'NEXUS_CRED' // Remplacez par l'ID de vos informations d'identification Nexus dans Jenkins
                    nexusPublisher nexusInstanceId: nexusCredentialId, nexusUrl: nexusUrl, repository: nexusRepository, version: '1.0-SNAPSHOT', groupId: 'com..mycompany.app', artifactId: 'my-app', packaging: 'jar', file: 'target/my-artifact.jar'

                }
            }
        }
       
            }
        }
    

