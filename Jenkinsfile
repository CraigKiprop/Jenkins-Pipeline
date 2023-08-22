pipeline {
    agent any
    
    stages {
        stage('Build') {
            steps {
                bat 'msbuild MyProject.sln'
            }
        }
        
        stage('Unit and Integration Tests') {
            steps {
                bat 'nunit3-console MyTests.dll'
            }
        }
        
        stage('Code Analysis') {
            steps {
                bat 'MSBuild.SonarQube.Runner.exe begin /k:"MyProject" /n:"My Project" /v:"1.0"'
                bat 'msbuild MyProject.sln'
                bat 'MSBuild.SonarQube.Runner.exe end'
            }
        }
        
        stage('Security Scan') {
            steps {
                bat 'zap-cli --scan <target>'
            }
        }
        
        stage('Deploy to Staging') {
            steps {
                bat 'powershell.exe -File deploy-staging.ps1'
            }
        }
        
        stage('Integration Tests on Staging') {
            steps {
                bat 'nunit3-console MyIntegrationTests.dll'
            }
        }
        
        stage('Deploy to Production') {
            steps {
                bat 'powershell.exe -File deploy-production.ps1'
            }
        }
    }
    
    post {
        always {
            emailext (
                subject: "Pipeline Status: ${currentBuild.currentResult}",
                body: "Pipeline status: ${currentBuild.currentResult}\n\nCheck attachment for logs.",
                to: 'craimokorir@email.com',
                attachLog: true,
            )
        }
    }
}
