pipeline {
    agent any

    environment {
        EMAIL_RECIPIENTS = 'wenchi9318@gmail.com'
    }

    options {
        skipDefaultCheckout true
        timestamps()
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

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
                    emailext (
                        subject: 'Jenkins: Test Stage Successful',
                        body: """<p>The <b>Test</b> stage completed <span style='color:green;'><b>successfully</b></span>.</p>
                                 <p>Job: ${env.JOB_NAME} #${env.BUILD_NUMBER}</p>
                                 <p>Check it <a href='${env.BUILD_URL}'>here</a>.</p>""",
                        to: "${env.EMAIL_RECIPIENTS}",
                        mimeType: 'text/html',
                        attachLog: true
                    )
                }
                failure {
                    emailext (
                        subject: 'Jenkins: Test Stage Failed',
                        body: """<p>The <b>Test</b> stage <span style='color:red;'><b>FAILED</b></span>.</p>
                                 <p>Job: ${env.JOB_NAME} #${env.BUILD_NUMBER}</p>
                                 <p>See details <a href='${env.BUILD_URL}'>here</a>.</p>""",
                        to: "${env.EMAIL_RECIPIENTS}",
                        mimeType: 'text/html',
                        attachLog: true
                    )
                }
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Performing security scan...'
            }
            post {
                always {
                    emailext (
                        subject: 'Jenkins: Security Scan Completed',
                        body: """<p><b>Security scan</b> stage completed.</p>
                                 <p>Job: ${env.JOB_NAME} #${env.BUILD_NUMBER}</p>
                                 <p>Link: <a href='${env.BUILD_URL}'>${env.BUILD_URL}</a></p>""",
                        to: "${env.EMAIL_RECIPIENTS}",
                        mimeType: 'text/html',
                        attachLog: true
                    )
                }
            }
        }
    }

    post {
        success {
            emailext (
                subject: "Jenkins Build #${env.BUILD_NUMBER} Success",
                body: """<p>The Jenkins job <b>${env.JOB_NAME}</b> completed <span style='color:green;'><b>successfully</b></span>.</p>
                         <p>Details: <a href='${env.BUILD_URL}'>Build #${env.BUILD_NUMBER}</a></p>""",
                to: "${env.EMAIL_RECIPIENTS}",
                mimeType: 'text/html',
                attachLog: true
            )
        }

        failure {
            emailext (
                subject: "Jenkins Build #${env.BUILD_NUMBER} Failed",
                body: """<p>The Jenkins job <b>${env.JOB_NAME}</b> <span style='color:red;'><b>FAILED</b></span>.</p>
                         <p>Details: <a href='${env.BUILD_URL}'>Build #${env.BUILD_NUMBER}</a></p>""",
                to: "${env.EMAIL_RECIPIENTS}",
                mimeType: 'text/html',
                attachLog: true
            )
        }
    }
}
