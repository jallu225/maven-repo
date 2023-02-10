node {
    stage ('Git Checkout') {
        git 'https://github.com/jallu225/webapp.git'
    }
    stage ('Unit Test'){
        sh "mvn test"
    }
    stage('Intergration Testing') {
        sh "mvn verify -DskipUnitTests"
    }
    stage ('Maven Build') {
        sh "mvn clean install"
    }
}
