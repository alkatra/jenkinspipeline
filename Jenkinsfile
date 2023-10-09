pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo '[NPM] Building the code using Node Package Manager'
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo '[JEST] Running Unit Test A'
                echo '[JEST] Unit Test A Successful'
                echo '[JEST] Running Unit Test B'
                echo '[JEST] Unit Test B Successful'
                echo '[JEST] Running Integration Test'
                echo '[JEST] Integration Test Successful'
            }
            post {
                success {
                    emailext(
                        to: 'sagargupta1827@gmail.com',
                        subject: "SUCCESS: Unit and Integration Tests",
                        body: """Tests completed successfully.""",
                        attachLog: true
                    )
                }
                failure {
                    emailext(
                        to: 'sagargupta1827@gmail.com',
                        subject: "FAILURE: Unit and Integration Tests",
                        body: """Tests failed. Check the attached logs.""",
                        attachLog: true
                    )
                }
            }
        }

        stage('Code Analysis') {
            steps {
                echo '[ESLint] Analyzing the code...'
                echo '[ESLint] Code analysis completed. 0 errors found.'
            }
        }

        stage('Security Scan') {
            steps {
                echo '[Snyk] Scanning the code for security vulnerabilities...'
            }
            post {
                success {
                    echo '[Snyk] Security scan completed without issues.'
                    emailext(
                        to: 'sagargupta1827@gmail.com',
                        subject: "SUCCESS: Security Scan",
                        body: """Security scan completed without issues.""",
                        attachLog: true
                    )
                }
                failure {
                    echo '[Snyk] Security scan detected vulnerabilities.'
                    emailext(
                        to: 'sagargupta1827@gmail.com',
                        subject: "FAILURE: Security Scan",
                        body: """Security scan detected vulnerabilities. See attached logs.""",
                        attachLog: true
                    )
                }
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to staging server on AWS EC2 instance.'
                echo 'Deployed successfully.'
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo '[JEST] Running integration tests on staging environment...'
                echo '[JEST] Integration tests completed successfully with no errors.'
            }
        }

        stage('Deploy to Production') {
            steps {
                echo 'Deploying to production server on AWS EC2 instance.'
            }
        }
    }

    post {
        always {
            echo 'Pipeline execution complete.'
        }
        success {
            echo 'Pipeline executed successfully!'
        }
        failure {
            echo 'Pipeline execution failed.'
        }
    }
}
