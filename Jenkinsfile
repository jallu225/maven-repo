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
    stage('Qulaity Gate Status'){
        waitForQualityGate abortPipeline: false, credentialsId: 'sonar'
    }
    stage('upload war file to nexus') {
     nexusArtifactUploader artifacts: [[artifactId: 'MavenWeb', classifier: '', file: 'target/MavenWeb.war', type: 'war']], credentialsId: 'nexus-cred', groupId: 'com.example', nexusUrl: '192.168.56.112:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'maven-web', version: '0.0.1'
    }
}
