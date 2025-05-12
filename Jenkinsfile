pipeline {
    agent any

    environment {
        EMAIL_RECIPIENTS = 'user@gmail.com'
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
                always {
                    script {
                        emailext(
                            subject: "Jenkins Build #${env.BUILD_NUMBER} - ${currentBuild.result}",
                            body: """
                                <h3>Job Details</h3>
                                <p><strong>Job:</strong> ${env.JOB_NAME}</p>
                                <p><strong>Build Number:</strong> ${env.BUILD_NUMBER}</p>
                                <p><strong>Status:</strong> ${currentBuild.result}</p>
                                <p><strong>URL:</strong> <a href="${env.BUILD_URL}">${env.BUILD_URL}</a></p>
                                <p>Test stage completed.</p>
                            """,
                            to: "${env.EMAIL_RECIPIENTS}",
                            attachLog: true,
                            mimeType: 'text/html'
                        )
                    }
                }
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Performing security scan...'
            }
            post {
                always {
                    script {
                        emailext(
                            subject: "Jenkins Build #${env.BUILD_NUMBER} - ${currentBuild.result}",
                            body: """
                                <h3>Security Scan Completed</h3>
                                <p><strong>Job:</strong> ${env.JOB_NAME}</p>
                                <p><strong>Build Number:</strong> ${env.BUILD_NUMBER}</p>
                                <p><strong>Status:</strong> ${currentBuild.result}</p>
                                <p><strong>URL:</strong> <a href="${env.BUILD_URL}">${env.BUILD_URL}</a></p>
                            """,
                            to: "${env.EMAIL_RECIPIENTS}",
                            attachLog: true,
                            mimeType: 'text/html'
                        )
                    }
                }
            }
        }
    }

    post {
        always {
            emailext(
                subject: "Jenkins Build #${env.BUILD_NUMBER} - ${currentBuild.result}",
                body: """
                    <h3>Final Build Status</h3>
                    <p><strong>Job:</strong> ${env.JOB_NAME}</p>
                    <p><strong>Build Number:</strong> ${env.BUILD_NUMBER}</p>
                    <p><strong>Status:</strong> ${currentBuild.result}</p>
                    <p><strong>URL:</strong> <a href="${env.BUILD_URL}">${env.BUILD_URL}</a></p>
                    <p>Build has finished. Check logs for details.</p>
                """,
                to: "${env.EMAIL_RECIPIENTS}",
                attachLog: true,
                mimeType: 'text/html'
            )
        }
    }
}
