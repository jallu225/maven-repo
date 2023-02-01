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
                    sh 'mvn test'
                }
            }
        }
        stage('Integration testing'){
            steps{
                script{   
                    sh 'mvn verify -DskipUnitTests'
                }
            }
        }
        stage('Maven Build'){
            steps {
                script {
                    sh "mvn clean install"
                }
            }
        }
        stage('Static code analysis'){
            steps{               
                script{
                    withSonarQubeEnv(credentialsId: 'sonar-token') { 
                        sh "mvn clean package sonar:sonar"
                    }
                }    
            }
        }
    }
}
