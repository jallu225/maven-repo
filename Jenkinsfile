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
    }
}
