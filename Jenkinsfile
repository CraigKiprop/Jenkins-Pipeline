pipeline {
    agent any
    
    stages {
        stage('Build') {
            steps {
                // Use your preferred build tool, e.g., MSBuild for .NET projects
                bat 'msbuild MyProject.sln'
            }
        }
        
        stage('Unit and Integration Tests') {
            steps {
                // Use your preferred test automation tools, e.g., NUnit
                bat 'nunit3-console MyTests.dll'
            }
        }
        
        stage('Code Analysis') {
            steps {
                // Integrate code analysis tool, e.g., SonarQube Scanner for MSBuild
                bat 'MSBuild.SonarQube.Runner.exe begin /k:"MyProject" /n:"My Project" /v:"1.0"'
                bat 'msbuild MyProject.sln'
                bat 'MSBuild.SonarQube.Runner.exe end'
            }
        }
        
        stage('Security Scan') {
            steps {
                // Integrate security scanning tool, e.g., OWASP ZAP
                bat 'zap-cli --scan <target>'
            }
        }
        
        stage('Deploy to Staging') {
            steps {
                // Use your deployment script or tool, e.g., PowerShell script
                bat 'deploy-staging.ps1'
            }
        }
        
        stage('Integration Tests on Staging') {
            steps {
                // Run integration tests on staging environment, e.g., NUnit
                bat 'nunit3-console MyIntegrationTests.dll'
            }
        }
        
        stage('Deploy to Production') {
            steps {
                // Use your deployment script or tool, e.g., PowerShell script
                bat 'deploy-production.ps1'
            }
        }
    }
    
    post {
        always {
            // Send notification emails with status and logs
            emailext (
                subject: "Pipeline Status: ${currentBuild.currentResult}",
                body: "Pipeline status: ${currentBuild.currentResult}\n\nCheck attachment for logs.",
                to: 'your@email.com',
                attachLog: true,
            )
        }
    }
}
