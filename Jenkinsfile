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
                    def nexusRepository = 'java-app' // Remplacez par le nom de votre repository Nexus
                    def nexusCredentialId = 'NEXUS_CRED' // Remplacez par l'ID de vos informations d'identification Nexus dans Jenkins

                    def server = Artifactory.server nexusUrl, nexusCredentialId
                    def rtMaven = Artifactory.newMavenBuild()

                    rtMaven.deployer server: server, releaseRepo: nexusRepository, snapshotRepo: nexusRepository
                    rtMaven.resolver server: server, releaseRepo: nexusRepository, snapshotRepo: nexusRepository

                    rtMaven.deployer.deployArtifacts = true
                    rtMaven.deployer.includePatterns = '**/*'
                    rtMaven.tool = 'M2_HOME' // Assurez-vous que 'Maven' est le nom de votre outil de build dans Jenkins
                    rtMaven.run rootPom: 'pom.xml', goals: 'clean deploy'
                }
            }
        }
       
            }
        }
    

