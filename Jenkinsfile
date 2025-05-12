pipeline {
    agent any

    environment {
        // Customize these
        EMAIL_RECIPIENT = 'wenchi9318@gmail.com'
        EMAIL_SUBJECT_PREFIX = 'Jenkins Job: '
    }

    options {
        buildDiscarder(logRotator(numToKeepStr: '10')) // clean old builds
        skipDefaultCheckout(true) // skip automatic SCM checkout
        timeout(time: 10, unit: 'MINUTES') // timeout if build hangs
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo '🔧 Building the application...'
                // Add build steps here
            }
        }

        stage('Test') {
            steps {
                echo '🧪 Running tests...'
                // Add test logic here
            }
            post {
                always {
                    emailext(
                        subject: "${EMAIL_SUBJECT_PREFIX} Test Stage Completed",
                        body: """<p><b>Test stage completed.</b></p><p>Job: ${env.JOB_NAME}<br>Build: #${env.BUILD_NUMBER}</p>""",
                        to: "${EMAIL_RECIPIENT}",
                        mimeType: 'text/html',
                        attachLog: true
                    )
                }
            }
        }

        stage('Security Scan') {
            steps {
                echo '🔍 Performing security scan...'
                // Add scan logic here
            }
            post {
                always {
                    emailext(
                        subject: "${EMAIL_SUBJECT_PREFIX} Security Scan Completed",
                        body: """<p><b>Security scan stage completed.</b></p><p>Job: ${env.JOB_NAME}<br>Build: #${env.BUILD_NUMBER}</p>""",
                        to: "${EMAIL_RECIPIENT}",
                        mimeType: 'text/html',
                        attachLog: true
                    )
                }
            }
        }
    }

    post {
        success {
            emailext(
                subject: "${EMAIL_SUBJECT_PREFIX} SUCCESS",
                body: """<p><b>Build succeeded!</b></p><p>Job: ${env.JOB_NAME}<br>Build: #${env.BUILD_NUMBER}</p>""",
                to: "${EMAIL_RECIPIENT}",
                mimeType: 'text/html'
            )
        }

        failure {
            emailext(
                subject: "${EMAIL_SUBJECT_PREFIX} FAILURE",
                body: """<p><b>Build failed.</b></p><p>Job: ${env.JOB_NAME}<br>Build: #${env.BUILD_NUMBER}</p>""",
                to: "${EMAIL_RECIPIENT}",
                mimeType: 'text/html',
                attachLog: true
            )
        }

        always {
            echo '📤 Post-build actions completed.'
        }
    }
}
