pipeline {
    agent any
    stages {
        stage('Test') {
            steps {
                echo "Running tests..."
                sh 'echo "This simulates a test process."'
            }
            post {
                always {
                    emailext (
                        to: 'wenchi9318@gmail.com',
                        subject: "Jenkins Test Stage Result: ${currentBuild.currentResult}",
                        body: """
                        <h3>Test Stage</h3>
                        <p>Status: ${currentBuild.currentResult}</p>
                        <p>Build: <a href="${env.BUILD_URL}">${env.BUILD_URL}</a></p>
                        """,
                        attachLog: true
                    )
                }
            }
        }

        stage('Security Scan') {
            steps {
                echo "Running security scan..."
                sh 'echo "This simulates a security scan."'
            }
            post {
                always {
                    emailext (
                        to: 'wenchi9318@gmail.com',
                        subject: "Jenkins Security Scan Result: ${currentBuild.currentResult}",
                        body: """
                        <h3>Security Scan</h3>
                        <p>Status: ${currentBuild.currentResult}</p>
                        <p>Build: <a href="${env.BUILD_URL}">${env.BUILD_URL}</a></p>
                        """,
                        attachLog: true
                    )
                }
            }
        }
    }
}
