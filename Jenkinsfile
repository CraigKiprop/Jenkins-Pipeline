pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo "Use a build automation tool like maven"
                // Add actual build steps here
            }
        }

        stage('Unit and Integration Test') {
            steps {
                echo "Use test automation tools for unit and integration tests"
                // Add actual test steps here

                // Create an empty file as a temporary attachment
                script {
                    def attachment = File.createTempFile("empty", ".txt")
                    attachment.text = "" // make it empty
                    currentBuild.rawBuild.addAction([attachment: attachment, filePath: attachment.name])
                }
            }
        }

        stage('Code Analysis') {
            steps {
                echo "Integrate a code analysis tool like SonarQube"
                // Add actual code quality check steps here
            }
        }

        stage('Security Scan') {
            steps {
                echo "Integrate a security scanning tool like OWASP ZAP"
                // Add actual security scan steps here
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo "Run integration tests in the staging environment"
                // Add actual deploy to staging steps here
            }
        }

        stage('Deploy to Production') {
            steps {
                echo "Deploy to production using Ansible or other tools"
                // Add actual deploy to production steps here
            }
        }
    }

    post {
        always {
            script {
                def attachmentsPattern = '**/*.log'

                // Attach the temporary file created in the Unit and Integration Test stage
                def attachmentAction = currentBuild.rawBuild.getAction([class: hudson.model.FileParameterValue])
                if (attachmentAction != null) {
                    emailext subject: "Integration Test Status",
                         body: "Integration test logs attached",
                         mimeType: 'text/plain',
                         to: "craigkorir@gmail.com",
                         attachmentsPattern: attachmentsPattern,
                         attachments: attachmentAction.filePath
                }
            }
        }
    }
}
