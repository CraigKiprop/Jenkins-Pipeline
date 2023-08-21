    pipeline {
    agent any
    
    stages {
        stage('Build') {
            steps {
                // Build the code using Maven
                sh 'mvn clean package'
            }
        }
        
        stage('Unit and Integration Tests') {
            steps {
                // Run unit tests and integration tests using appropriate test automation tools
                sh 'mvn test'
            }
        }
        
        stage('Code Analysis') {
            steps {
                // Integrate a code analysis tool (e.g., SonarQube)
                sh 'mvn sonar:sonar'
            }
        }
        
        stage('Security Scan') {
            steps {
                // Integrate a security scanning tool (e.g., OWASP ZAP)
                sh 'zap-cli --spider <https://github.com/CraigKiprop/Deakin-Unit-Page>'
                sh 'zap-cli --scan <https://github.com/CraigKiprop/Deakin-Unit-Page>'
            }
        }
        
        stage('Deploy to Staging') {
            steps {
                // Deploy the application to staging server (e.g., AWS EC2 instance) using Ansible
                sh 'ansible-playbook -i inventory/staging deploy.yml'
            }
        }
        
        stage('Integration Tests on Staging') {
            steps {
                // Run integration tests in the staging environment
                sh 'mvn verify -Pstaging'
            }
        }
        
        stage('Deploy to Production') {
            steps {
                // Deploy the application to production server (e.g., AWS EC2 instance) using Ansible
                sh 'ansible-playbook -i inventory/production deploy.yml'
            }
        }
    }
    
    post {
        always {
            // Archive artifacts
            archiveArtifacts artifacts: '**/target/*.jar', allowEmptyArchive: true
            
            // Send email notifications
            emailext (
                subject: "Pipeline ${currentBuild.currentResult}: ${env.JOB_NAME}",
                body: "Pipeline ${currentBuild.currentResult}: ${env.JOB_NAME}\n\nCheck attached logs.",
                to: 'your@email.com',
                attachmentsPattern: '**/*.log'
            )
        }
    }
}
