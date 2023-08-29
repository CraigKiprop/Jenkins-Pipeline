pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo "Use a build automation tool like maven"
                // Replace with your actual build commands
            }
        }

        stage('Unit and Integration Test') {
            steps {
                echo "Use test automation tools for unit and integration tests"
                // Run your test automation commands here

                // Archive necessary artifacts
                archiveArtifacts artifacts: '**/target/*.jar', allowEmptyArchive: true

                // List .jar files in the workspace
                def jarFiles = bat(script: "dir /S /B %WORKSPACE%\\*.jar", returnStdout: true).trim()

                // Save the list of jar files to a text file
                writeFile file: 'jar_files.txt', text: jarFiles
            }
            post {
                always {
                    script {
                        // Read the list of jar files from the text file
                        def jarFiles = readFile('jar_files.txt')

                        emailext body: "Unit and Integration test ${currentBuild.result}\n\nJar files attached.",
                                 mimeType: 'text/plain',
                                 subject: "Unit and Integration Test Status - ${currentBuild.result}",
                                 to: 'craigkorir@gmail.com',
                                 attachmentsPattern: jarFiles
                    }
                }
            }
        }

        stage('Code Analysis') {
            steps {
                echo "Integrate a code analysis tool like SonarQube"
                // Replace with your actual code analysis commands
            }
        }

        stage('Security Scan') {
            steps {
                echo "Integrate a security scanning tool like OWASP ZAP"
                // Replace with your actual security scan commands
            }
            post {
                always {
                    script {
                        // Similar email configuration as Unit and Integration Test stage
                    }
                }
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo "Run integration tests in the staging environment"
                // Replace with your actual deployment and testing commands for staging
            }
        }

        stage('Deploy to Production') {
            steps {
                echo "Deploy to production using Ansible or other tools"
                // Replace with your actual deployment commands for production
            }
        }
    }

    post {
        always {
            // Archive artifacts
            archiveArtifacts artifacts: '**/target/*.jar', allowEmptyArchive: true
        }
    }
}
