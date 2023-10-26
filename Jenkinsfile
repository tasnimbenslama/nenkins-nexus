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
    def artifactPath = 'target/my-artifact.jar'
                    def nexusUrl = env.NEXUS_URL
                    def nexusRepo = env.NEXUS_REPOSITORY

                    withCredentials([usernamePassword(credentialsId: 'NEXUS_CRED', usernameVariable: 'admin', passwordVariable: 'admin123')]) {
                        sh "curl -v -u $NEXUS_USERNAME:$NEXUS_PASSWORD --upload-file $artifactPath $nexusUrl/repository/$nexusRepo/com/example/my-artifact/1.0/my-artifact-1.0.jar"
                }
            }
        }
       
            }
        }
    

