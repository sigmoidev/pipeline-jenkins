pipeline {
agent any
// test
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

  stage('Documentation') {
      steps {
          script {
              bat './mvnw javadoc:javadoc'

              bat 'if exist doc rmdir /S /Q doc'
              bat 'mkdir doc'

              bat 'xcopy /E /I /Y target\\site doc'

              bat 'powershell -Command "Compress-Archive -Path doc\\* -DestinationPath doc.zip"'

              archiveArtifacts artifacts: 'doc.zip', fingerprint: true
          }
      }

  }

}
stage('html') {
    steps {

                always {
                     publishHTML (target : [allowMissing: false,
                      alwaysLinkToLastBuild: true,
                      keepAll: true,
                      reportFiles: 'target/site/apidocs',
                      reportName: 'index.html',
                      reportTitles: 'Documentation Report'])
                  }
    }

}
}