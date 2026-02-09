pipeline {
    agent any
//comment
// test
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Init') {
            steps {
                bat './mvnw clean'
            }
        }

        stage('Test') {
            steps {
                bat './mvnw test'
                junit '**/target/surefire-reports/*.xml'
            }
        }

//        stage('Documentation') {
//            steps {
//                script {
//                    bat './mvnw javadoc:javadoc'
//                    // Clean up previous 'doc' folder if it exists
//                    bat 'if exist doc rmdir /S /Q doc'
//                    bat 'mkdir doc'
//                    // Copy Javadoc content to the 'doc' folder
//                    bat 'xcopy /E /I /Y target\\site doc'
//                    // Delete existing doc.zip if it exists
//                    bat 'if exist doc.zip del /Q doc.zip'
//                    // Create the ZIP file with the new content
//                    bat 'powershell -Command "Compress-Archive -Path doc\\* -DestinationPath doc.zip -Force"'
//                    // Archive the doc.zip file for Jenkins artifacts
//                    archiveArtifacts artifacts: 'doc.zip', fingerprint: true
//                }
//            }
//        }

        stage('Build') {
            steps {
                bat './mvnw install'
                archiveArtifacts artifacts: 'target/*.jar'
            }
        }
//comments
        stage('Deploy') {
            steps {
              bat 'docker-compose up --build -d'
//                echo 'Deploying...'
//                  mail (
//                                subject: "Build ${currentBuild.currentResult}: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'",
//                                body: """<p>Build ${currentBuild.currentResult}: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'</p>
//                                         <p>Check console output at <a href="${env.BUILD_URL}console">this link</a> for details.</p>""",
//                               // recipientProviders: [[$class: 'DevelopersRecipientProvider']],
//                                to: 'ha.deboub.cntsid@gmail.com'
//                            )
            }
        }
    }
    //add some comment
//
//    post {
//        always {
//            emailext (
//                subject: "Build ${currentBuild.currentResult}: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'",
//                body: """<p>Build ${currentBuild.currentResult}: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'</p>
//                         <p>Check console output at <a href="${env.BUILD_URL}console">this link</a> for details.</p>""",
//                recipientProviders: [[$class: 'DevelopersRecipientProvider']],
//                to: 'ha.deboub.cntsid@gmail.com'
//            )
//        }
//        success {
//            // Success-related actions can go here if needed
//            emailext (
//                            subject: "Build ${currentBuild.currentResult}: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'",
//                            body: """<p>Build ${currentBuild.currentResult}: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'</p>
//                                     <p>Check console output at <a href="${env.BUILD_URL}console">this link</a> for details.</p>""",
//                            recipientProviders: [[$class: 'DevelopersRecipientProvider']],
//                            to: 'ha.deboub.cntsid@gmail.com'
//                        )
//        }
//        failure {
//            // Failure-related actions can go here if needed
//            emailext (
//                subject: "Build ${currentBuild.currentResult}: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'",
//                body: """<p>Build ${currentBuild.currentResult}: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'</p>
//                         <p>Check console output at <a href="${env.BUILD_URL}console">this link</a> for details.</p>""",
//                recipientProviders: [[$class: 'DevelopersRecipientProvider']],
//                to: 'ha.deboub.cntsid@gmail.com'
//            )
//        }
//    }
}
