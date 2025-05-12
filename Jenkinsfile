pipeline {
    agent any

    environment {
        EMAIL_RECIPIENTS = 'wenchi9318@gmail.com'
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
                        subject: 'Test Stage Completed Successfully',
                        body: "The Test stage was successful. Job: ${env.JOB_NAME} Build: #${env.BUILD_NUMBER}",
                        to: "${env.EMAIL_RECIPIENTS}",
                        attachLog: true
                    )
                }
                failure {
                    emailext(
                        subject: 'Test Stage Failed',
                        body: "The Test stage failed. Job: ${env.JOB_NAME} Build: #${env.BUILD_NUMBER}",
                        to: "${env.EMAIL_RECIPIENTS}",
                        attachLog: true
                    )
                }
            }
        }
    }

    post {
        always {
            emailext(
                subject: "Build #${env.BUILD_NUMBER} Status",
                body: "Build Status: ${currentBuild.currentResult}\nCheck the logs for details.\nJob: ${env.JOB_NAME}",
                to: "${env.EMAIL_RECIPIENTS}",
                attachLog: true
            )
        }
    }
}
