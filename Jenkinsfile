pipeline {
    agent any
    stages {
        stage ('Git Checkout') {
            steps {
                script{
                    git branch: 'main', url: 'https://github.com/jallu225/maven-repo.git'
                }
            }
        }
        stage ('UNIT Testing') {
            steps {
                script{
                    bat 'mvn test'
                }
            }
        }
        stage('Integration testing'){
            steps{
                script{   
                    bat 'mvn verify -DskipUnitTests'
                }
            }
        }
        stage('Maven Build'){
            steps {
                script {
                    bat "mvn clean install"
                }
            }
        }
        stage('Static code analysis'){
            steps{               
                script{
                    withSonarQubeEnv(credentialsId: 'sonar-token') { 
                        bat "mvn clean package sonar:sonar"
                    }
                }    
            }
        }
        stage('Quality gate Status'){
            steps {
                script{
                    waitForQualityGate abortPipeline: false, credentialsId: 'sonar-token'
                }
            }
        }
        stage('artifacts upload'){
            steps{
                script{
                    nexusArtifactUploader artifacts: [[artifactId: 'MavenWeb', classifier: '', file: 'target/MavenWeb.war', type: 'war']], credentialsId: 'nexus-cred', groupId: 'com.example', nexusUrl: '192.168.56.112:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'maven-web', version: '0.0.1'
                }
            }
        }
    }
}
