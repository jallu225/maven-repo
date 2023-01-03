pipeline {
    agent any
    stages {
        stage ('Git Checkout') {
            steps {
                script{
                    git branch: 'main', url: 'https://github.com/jallu225/demo-counter-app.git'
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
    }
}
