pipeline {
    agent any
    
    stages {
        stage('Build') {
            steps {
                // Use a build automation tool like Maven
                sh 'mvn clean package'
            }
        }
        
        stage('Unit and Integration Tests') {
            steps {
                // Use test automation tools for unit and integration tests
                sh 'mvn test'
            }
        }
        
        stage('Code Analysis') {
            steps {
                // Integrate a code analysis tool like SonarQube
                sh 'mvn sonar:sonar'
            }
        }
        
        stage('Security Scan') {
            steps {
                // Integrate a security scanning tool like OWASP ZAP
                sh 'zap-cli --spider <your_app_url>'
                sh 'zap-cli --scan <your_app_url>'
            }
        }
        
        stage('Deploy to Staging') {
            steps {
                // Use a deployment tool to deploy to staging, like Ansible
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
                // Deploy to production using Ansible or other tools
                sh 'ansible-playbook -i inventory/production deploy.yml'
            }
        }
    }
    
    post {
        always {
            // Archive artifacts, send email notifications, etc.
            archiveArtifacts artifacts: '**/target/*.jar', allowEmptyArchive: true
            
            // Send email notifications
            emailext (
                subject: "Pipeline ${currentBuild.currentResult}: ${env.JOB_NAME}",
                body: "Pipeline ${currentBuild.currentResult}: ${env.JOB_NAME}\n\nCheck attached logs.",
                to: 'craigkorir@email.com',
                attachmentsPattern: '**/*.log'
            )
        }
    }
}
