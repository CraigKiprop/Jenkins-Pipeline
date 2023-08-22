pipeline {
    agent any
    
    stages {
        stage('Build') {
            steps {
                // Use your preferred build tool, e.g., Maven
                sh 'mvn clean package'
            }
        }
        
        stage('Unit and Integration Tests') {
            steps {
                // Use your preferred test automation tools
                sh 'mvn test'
            }
        }
        
        stage('Code Analysis') {
            steps {
                // Integrate code analysis tool, e.g., SonarQube
                sh 'sonar-scanner'
            }
        }
        
        stage('Security Scan') {
            steps {
                // Integrate security scanning tool, e.g., OWASP ZAP
                sh 'zap-cli --scan <target>'
            }
        }
        
        stage('Deploy to Staging') {
            steps {
                // Use your deployment script or tool
                sh 'deploy-staging.sh'
            }
        }
        
        stage('Integration Tests on Staging') {
            steps {
                // Run integration tests on staging environment
                sh 'mvn integration-test'
            }
        }
        
        stage('Deploy to Production') {
            steps {
                // Use your deployment script or tool
                sh 'deploy-production.sh'
            }
        }
    }
    
    post {
        always {
            // Send notification emails with status and logs
            emailext (
                subject: "Pipeline Status: ${currentBuild.currentResult}",
                body: "Pipeline status: ${currentBuild.currentResult}\n\nCheck attachment for logs.",
                to: 'craigkorir@gmail.com',
                attachLog: true,
            )
        }
    }
}
