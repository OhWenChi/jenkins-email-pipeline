pipeline {
    agent any

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
                        emailext to: 'wenchi9318@gmail.com',
                            subject: "Test Stage Completed",
                            body: "The test stage completed successfully.",
                            attachLog: true
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
                        emailext to: 'wenchi9318@gmail.com',
                            subject: "Security Scan Completed",
                            body: "The security scan stage finished.",
                            attachLog: true
                    }
                }
            }
        }
    }
}
