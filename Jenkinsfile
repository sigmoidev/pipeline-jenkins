pipeline {
agent any
stages {
    stage('Test') {
        steps {

            junit 'target/surefire-reports/*.xml'
        }
    }
    stage('Build') {
        steps {
            bat './mvnw clean install'
            archiveArtifacts artifacts: 'target/*.jar'
        }
    }
    stage('documentation') {
            steps {
                bat './mvnw javadoc:javadoc'
                archiveArtifacts artifacts: 'target/site/apidocs/**'
            }
        }

}
}