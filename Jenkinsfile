pipeline {
    agent any

    environment {
        EMAIL_RECIPIENTS = 'wenchi9318@gmail.com'
    }

    stages {
        stage('Build') {
            steps {
                echo 'Tool: Maven used to build the Java application'
                echo 'Building the application...'
                // Example command: sh 'mvn clean install'
            }
        }

        stage('Test') {
            steps {
                echo 'Tool: JUnit used for unit testing'
                echo 'Running tests...'
                // Example command: sh 'mvn test'
            }
            post {
                success {
                    script {
                        emailext(
                            subject: "Jenkins Build #${env.BUILD_NUMBER} - TEST STAGE SUCCESS",
                            body: """
                                <h3>Test Stage - Success</h3>
                                <p><strong>Job:</strong> ${env.JOB_NAME}</p>
                                <p><strong>Build Number:</strong> ${env.BUILD_NUMBER}</p>
                                <p><strong>URL:</strong> <a href="${env.BUILD_URL}">${env.BUILD_URL}</a></p>
                                <p>The test stage completed successfully.</p>
                            """,
                            to: "${env.EMAIL_RECIPIENTS}",
                            attachLog: true,
                            mimeType: 'text/html'
                        )
                    }
                }
                failure {
                    script {
                        emailext(
                            subject: "Jenkins Build #${env.BUILD_NUMBER} - TEST STAGE FAILED",
                            body: """
                                <h3>Test Stage - Failure</h3>
                                <p><strong>Job:</strong> ${env.JOB_NAME}</p>
                                <p><strong>Build Number:</strong> ${env.BUILD_NUMBER}</p>
                                <p><strong>URL:</strong> <a href="${env.BUILD_URL}">${env.BUILD_URL}</a></p>
                                <p>The test stage failed. Please check the attached logs.</p>
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
                echo 'Tool: OWASP Dependency-Check used for security scanning'
                echo 'Performing security scan...'
                // Example command: sh './dependency-check.sh'
            }
            post {
                success {
                    script {
                        emailext(
                            subject: "Jenkins Build #${env.BUILD_NUMBER} - SECURITY SCAN SUCCESS",
                            body: """
                                <h3>Security Scan - Success</h3>
                                <p><strong>Job:</strong> ${env.JOB_NAME}</p>
                                <p><strong>Build Number:</strong> ${env.BUILD_NUMBER}</p>
                                <p><strong>URL:</strong> <a href="${env.BUILD_URL}">${env.BUILD_URL}</a></p>
                                <p>The security scan completed successfully.</p>
                            """,
                            to: "${env.EMAIL_RECIPIENTS}",
                            attachLog: true,
                            mimeType: 'text/html'
                        )
                    }
                }
                failure {
                    script {
                        emailext(
                            subject: "Jenkins Build #${env.BUILD_NUMBER} - SECURITY SCAN FAILED",
                            body: """
                                <h3>Security Scan - Failure</h3>
                                <p><strong>Job:</strong> ${env.JOB_NAME}</p>
                                <p><strong>Build Number:</strong> ${env.BUILD_NUMBER}</p>
                                <p><strong>URL:</strong> <a href="${env.BUILD_URL}">${env.BUILD_URL}</a></p>
                                <p>The security scan stage failed. Please check the attached logs.</p>
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
                subject: "Jenkins Build #${env.BUILD_NUMBER} - FINAL STATUS: ${currentBuild.currentResult}",
                body: """
                    <h3>Final Build Status</h3>
                    <p><strong>Job:</strong> ${env.JOB_NAME}</p>
                    <p><strong>Build Number:</strong> ${env.BUILD_NUMBER}</p>
                    <p><strong>Status:</strong> ${currentBuild.currentResult}</p>
                    <p><strong>URL:</strong> <a href="${env.BUILD_URL}">${env.BUILD_URL}</a></p>
                    <p>Build has finished. Check logs for more details.</p>
                """,
                to: "${env.EMAIL_RECIPIENTS}",
                attachLog: true,
                mimeType: 'text/html'
            )
        }
    }
}
