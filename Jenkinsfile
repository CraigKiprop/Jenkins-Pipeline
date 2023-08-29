pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo "Building the code using Maven"
                sh 'mvn clean package'
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo "Running unit tests"
                sh 'mvn test' // Assuming Maven is configured for tests
                
                echo "Running integration tests"
                // Add commands to run integration tests here
            }
            post {
                always {
                    archiveArtifacts artifacts: '**/*.log', allowEmptyArchive: true
                    emailext (
                        to: 'craigkorir@gmail.com',
                        subject: "Unit and Integration Test Status - ${currentBuild.result}",
                        body: "Unit and Integration test ${currentBuild.result}",
                        attachmentsPattern: '**/*.log',
                        mimeType: 'text/plain',
                        recipientProviders: [[$class: 'CulpritsRecipientProvider']]
                    )
                }
            }
        }

        stage('Code Analysis') {
            steps {
                echo "Running code analysis using SonarQube"
                // Add commands to run code analysis using SonarQube here
            }
        }

        stage('Security Scan') {
            steps {
                echo "Performing security scan using OWASP ZAP"
                // Add commands to run security scan using OWASP ZAP here
            }
            post {
                always {
                    archiveArtifacts artifacts: '**/*.log', allowEmptyArchive: true
                    emailext (
                        to: 'craigkorir@gmail.com',
                        subject: "Security Scan Status - ${currentBuild.result}",
                        body: "Security scan ${currentBuild.result}",
                        attachmentsPattern: '**/*.log',
                        mimeType: 'text/plain',
                        recipientProviders: [[$class: 'CulpritsRecipientProvider']]
                    )
                }
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo "Deploying to staging server (e.g., AWS EC2)"
                // Add commands to deploy to staging server here
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo "Running integration tests on staging"
                // Add commands to run integration tests on staging environment here
            }
        }

        stage('Deploy to Production') {
            steps {
                echo "Deploying to production server (e.g., AWS EC2)"
                // Add commands to deploy to production server here
            }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: '**/*.log', allowEmptyArchive: true
        }
    }
}
