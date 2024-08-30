pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building the code...'
                // Use a build automation tool, e.g., Maven
                // Example: sh 'mvn clean install'
                echo 'Build tool: Maven (or other appropriate tool)'
            }
        }
        
        stage('Unit and Integration Tests') {
            steps {
                echo 'Running unit and integration tests...'
                // Test automation tools like JUnit or TestNG
                // Example: sh 'mvn test'
                echo 'Test automation tool: JUnit or TestNG'
            }
            post {
                always {
                    script {
                        def buildStatus = currentBuild.currentResult
                        def emailSubject = "Unit and Integration Tests: ${buildStatus}"
                        def emailBody = "Unit and Integration Tests stage ${buildStatus}.\n\nPlease find the attached logs for details."
                        
                        emailext (
                            to: 'adamjago7@gmail.com',
                            subject: emailSubject,
                            body: emailBody,
                            attachLog: true
                        )
                    }
                }
            }
        }
        
        stage('Code Analysis') {
            steps {
                echo 'Running code analysis...'
                // Code analysis tool like SonarQube
                // Example: sh 'sonar-scanner'
                echo 'Code analysis tool: SonarQube'
            }
        }
        
        stage('Security Scan') {
            steps {
                echo 'Performing security scan...'
                // Security scan tool like OWASP ZAP or Snyk
                // Example: sh 'zap-cli start'
                echo 'Security scan tool: OWASP ZAP or Snyk'
            }
            post {
                always {
                    script {
                        def buildStatus = currentBuild.currentResult
                        def emailSubject = "Security Scan: ${buildStatus}"
                        def emailBody = "Security Scan stage ${buildStatus}.\n\nPlease find the attached logs for details."
                        
                        emailext (
                            to: 'adamjago7@gmail.com',
                            subject: emailSubject,
                            body: emailBody,
                            attachLog: true
                        )
                    }
                }
            }
        }
        
        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to staging...'
                // Deployment command to staging server
                // Example: sh 'deploy.sh staging'
                echo 'Deployment tool: Staging deployment script'
            }
        }
        
        stage('Integration Tests on Staging') {
            steps {
                echo 'Running integration tests on staging...'
                // Perform integration tests on the staging server
                // Example: sh 'integration-test.sh staging'
                echo 'Integration tests on staging server'
            }
        }
        
        stage('Deploy to Production') {
            steps {
                echo 'Deploying to production...'
                // Deployment command to production server
                // Example: sh 'deploy.sh production'
                echo 'Deployment tool: Production deployment script'
            }
        }
    }

    post {
        always {
            script {
                def buildStatus = currentBuild.currentResult
                def emailSubject = "${buildStatus}: Pipeline Execution Report"
                def emailBody = "The pipeline ${buildStatus}.\n\nPlease find the attached logs for details."
                
                emailext (
                    to: 'adamjago7@gmail.com',
                    subject: emailSubject,
                    body: emailBody,
                    attachLog: true
                )
            }
        }
        
        failure {
            script {
                emailext(
                    to: 'adamjago7@gmail.com',
                    subject: 'Pipeline Failed',
                    body: 'The pipeline failed during one of the stages. Check the logs for more details.',
                    attachLog: true
                )
            }
        }
        
        success {
            script {
                emailext(
                    to: 'adamjago7@gmail.com',
                    subject: 'Pipeline Succeeded',
                    body: 'The pipeline has successfully completed.',
                    attachLog: true
                )
            }
        }
    }
}
