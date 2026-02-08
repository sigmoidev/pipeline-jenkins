pipeline {
agent any
stages {
    stage('Build') {
        steps {
            bat './mvnw clean install'
            archiveArtifacts artifacts: 'target/*.jar'
        }
    }
//    stage('Test') {
//        steps {
//            echo 'Testing...'
//        }
//    }
//    stage('Deploy') {
//        steps {
//            echo 'Deploying...'
//        }
//    }
}
}