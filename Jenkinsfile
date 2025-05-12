pipeline {
    agent any

    environment {
        EMAIL_RECIPIENTS = 'wenchi9318@gmail.com'
        EMAIL_SUBJECT = "Jenkins Build #${env.BUILD_NUMBER} - ${currentBuild.result}"
        EMAIL_BODY = "Job: ${env.JOB_NAME}\nBuild Number: ${env.BUILD_NUMBER}\nStatus: ${currentBuild.result}\nURL: ${env.BUILD_URL}"
    }

    stages {
        stage('Build') {
            steps {
                echo 'Building the application...'
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
            }
            post {
                success {
                    emailext(
                        subject: "${env.EMAIL_SUBJECT}",
                        body: "${env.EMAIL_BODY}\nTest stage completed successfully.",
                        to: "${env.EMAIL_RECIPIENTS}",
                        attachLog: true,
                        mimeType: 'text/plain'  // Ensures plain text formatting
                    )
                }
                failure {
                    emailext(
                        subject: "${env.EMAIL_SUBJECT}",
                        body: "${env.EMAIL_BODY}\nTest stage failed.",
                        to: "${env.EMAIL_RECIPIENTS}",
                        attachLog: true,
                        mimeType: 'text/plain'
                    )
                }
            }
        }
    }

    post {
        always {
            emailext(
                subject: "${env.EMAIL_SUBJECT}",
                body: "${env.EMAIL_BODY}\nBuild has finished. Check the logs for more details.",
                to: "${env.EMAIL_RECIPIENTS}",
                attachLog: true,
                mimeType: 'text/plain'
            )
        }
    }
}
