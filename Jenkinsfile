pipeline {
    agent any
    
    stages {
        stage('Build') {
            steps {
                script {
                    // Build automation tool: MSBuild
                    bat 'msbuild MyProject.sln'
                }
            }
        }
        
        stage('Unit and Integration Tests') {
            steps {
                script {
                    // Test automation tool: NUnit for unit tests, MSTest for integration tests
                    bat 'nunit3-console MyTests.dll'
                    bat 'mstest /testcontainer:MyIntegrationTests.dll'
                }
            }
        }
        
        stage('Code Analysis') {
            steps {
                script {
                    // Code analysis tool: SonarQube Scanner for MSBuild
                    bat 'MSBuild.SonarQube.Runner.exe begin /k:"MyProject" /n:"My Project" /v:"1.0"'
                    bat 'msbuild MyProject.sln'
                    bat 'MSBuild.SonarQube.Runner.exe end'
                }
            }
        }
        
        stage('Security Scan') {
            steps {
                script {
                    // Security scanning tool: OWASP ZAP
                    bat 'zap-cli --scan <target>'
                }
            }
        }
        
        stage('Deploy to Staging') {
            steps {
                script {
                    // Deployment tool: PowerShell script for AWS deployment
                    bat 'powershell.exe -File deploy-staging.ps1'
                }
            }
        }
        
        stage('Integration Tests on Staging') {
            steps {
                script {
                    // Run integration tests on staging environment using MSTest
                    bat 'mstest /testcontainer:MyStagingIntegrationTests.dll'
                }
            }
        }
        
        stage('Deploy to Production') {
            steps {
                script {
                    // Deployment tool: PowerShell script for AWS deployment
                    bat 'powershell.exe -File deploy-production.ps1'
                }
            }
        }
    }
    
    post {
        success {
            script {
                // Send success email with logs
                emailext (
                    subject: "Pipeline Success",
                    body: "The pipeline completed successfully. Check attachment for logs.",
                    to: 'craigkorir@email.com',
                    attachLog: true,
                )
            }
        }
        failure {
            script {
                // Send failure email with logs
                emailext (
                    subject: "Pipeline Failed",
                    body: "The pipeline failed. Check attachment for logs.",
                    to: 'craigkorir@email.com',
                    attachLog: true,
                )
            }
        }
    }
}
