pipeline {
    agent any
    stages {
        stage('Preparation') {
            parallel {
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
            }
        }

        stage('Test') {
            steps {
                bat './mvnw test'
                junit '**/target/surefire-reports/*.xml'
            }
        }

        // Documentation stage has been commented out for clarity; uncomment if needed
        /*
        stage('Documentation') {
            steps {
                script {
                    bat './mvnw javadoc:javadoc'
                    bat 'if exist doc rmdir /S /Q doc'
                    bat 'mkdir doc'
                    bat 'xcopy /E /I /Y target\\site doc'
                    bat 'if exist doc.zip del /Q doc.zip'
                    bat 'powershell -Command "Compress-Archive -Path doc\\* -DestinationPath doc.zip -Force"'
                    archiveArtifacts artifacts: 'doc.zip', fingerprint: true
                }
            }
        }
        */

        stage('Build') {
            steps {
                bat './mvnw install'
                archiveArtifacts artifacts: 'target/*.jar'
            }
        }

        stage('Deploy') {
            when {
                branch 'second-branche' // Ensure the branch name matches exactly
            }
            steps {
                bat 'docker-compose up --build -d'
                // Uncomment if you want to send a notification email
                /*
                mail (
                    subject: "Build ${currentBuild.currentResult}: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'",
                    body: """<p>Build ${currentBuild.currentResult}: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'</p>
                             <p>Check console output at <a href="${env.BUILD_URL}console">this link</a> for details.</p>""",
                    to: 'ha.deboub.cntsid@gmail.com'
                )
                */
            }
        }
    }

    // Optional post section for email notifications can be included
    /*
    post {
        always {
            emailext (
                subject: "Build ${currentBuild.currentResult}: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'",
                body: """<p>Build ${currentBuild.currentResult}: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'</p>
                         <p>Check console output at <a href="${env.BUILD_URL}console">this link</a> for details.</p>""",
                recipientProviders: [[$class: 'DevelopersRecipientProvider']],
                to: 'ha.deboub.cntsid@gmail.com'
            )
        }
        success {
            emailext (
                subject: "SUCCESS: Build ${currentBuild.currentResult}: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'",
                body: """<p>Build Success: '${env.JOB_NAME} [${env.BUILD_NUMBER}]'</p>
                         <p>Check console output at <a href="${env.BUILD_URL}console">this link</a> for details.</p>""",
                recipientProviders: [[$class: 'DevelopersRecipientProvider']],
                to: 'ha.deboub.cntsid@gmail.com'
            )
        }
        failure {
            emailext (
                subject: "FAILURE: Build ${currentBuild.currentResult}: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'",
                body: """<p>Build Failure: '${env.JOB_NAME} [${env.BUILD_NUMBER}]'</p>
                         <p>Check console output at <a href="${env.BUILD_URL}console">this link</a> for details.</p>""",
                recipientProviders: [[$class: 'DevelopersRecipientProvider']],
                to: 'ha.deboub.cntsid@gmail.com'
            )
        }
    }
    */
}