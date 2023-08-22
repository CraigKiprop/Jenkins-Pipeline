pipeline {
    agent any

        stages {
        stage('Build') {
            steps {
                echo "Use a build automation tool like maven"
                echo "bat 'mvn clean package'"
                // Add actual build steps here
            }
            
            }
        }

        stage('Unit and intergration Test') {
            steps {
                echo "Use test automation tools for unit and intergration testUnit tests"
                echo "sh 'mvn test'"
                // Add actual test steps here
            }
            post{
                always{
                        mail to: "craigkorir@gmail.com",
                        subject: "Build Status",
                        body: "build log attached"
                }
        }

        stage('Code Analysis') {
            steps {
                echo "Integrate a code analysis tool like SonarQube"
                echo "sh 'mvn sonar:sonar'"
                // Add actual code quality check steps here
            }
        }

        stage('Security Scan') {
            steps {
                echo "Integrate a security scanning tool like OWASP ZAP)."
                // sh 'zap-cli --spider <your_app_url>'
            }
            post {
        success {
            // Send email notifications on success
            emailext (
                subject: "Pipeline Successful: ${env.JOB_NAME}",
                body: "The pipeline has completed successfully.",
                to: 'craigkorir@gmail.com',
                attachmentsPattern: '**/*.log'
            )
        }
        failure {
            // Send email notifications on failure
            emailext (
                subject: "Pipeline Failed: ${env.JOB_NAME}",
                body: "The pipeline has failed. Please check the attached logs for details.",
                to: 'craigkorir@gmail.com',
                attachmentsPattern: '**/*.log'
            )
        }
        }

        stage('Deploy to Staging') {
            steps {
                echo "Run integration tests in the staging environment."
                // sh 'mvn verify -Pstaging
            }
        }
            stage('Deploy to production') {
            steps {
                echo " Deploy to production using Ansible or other tools"
                // sh 'ansible-playbook -i inventory/production deploy.yml'
                
            }
        }
            
    }
}

}
