node {
    stage ('Git Checkout'){
       git branch: 'dev', url: 'https://github.com/jallu225/maven-repo.git'
    }
    stage ('Unit test') {
        bat 'mvn test'
    }
    stage('Integration Testing'){
        bat "mvn verify -DskipUnitTests"
    }
    stage ('Maven build') {
        bat 'mvn clean install'
    }
    stage('Static code analysis'){
        withSonarQubeEnv(credentialsId: 'sonar') { 
            bat "mvn clean package sonar:sonar"
         }
    }  
}
