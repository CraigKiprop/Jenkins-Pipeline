pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo "Use a build automation tool like maven"
                //bat 'mvn clean package'
                // Add actual build steps here
            }
        }

        stage('Unit and Integration Test') {
    steps {
        echo "Use test automation tools for unit and integration tests"
        // Add actual test steps here
        archiveArtifacts artifacts: '**', allowEmptyArchive: true
    }
    post {
        always {
            emailext(
                subject: "Unit and Integration Test Status - ${currentBuild.result}",
                body: "Unit and Integration test ${currentBuild.result}",
                to: "craigkorir@gmail.com",
                attachmentsPattern: '**',  // Attach all files
                attachLog: true
            )
        }
    }
}

        stage('Code Analysis') {
            steps {
                echo "Integrate a code analysis tool like SonarQube"
                //sh 'mvn sonar:sonar'
                // Add actual code quality check steps here
            }
        }

        stage('Security Scan') {
    steps {
        echo "Integrate a security scanning tool like OWASP ZAP"
        // Add security scan steps here
    }
    post {
        always {
            emailext(
                subject: "Security Scan Status - ${currentBuild.result}",
                body: "Security scan ${currentBuild.result}",
                to: "craigkorir@gmail.com",
                attachmentsPattern: '**',  // Attach all files
                attachLog: true
            )
        }
    }
}

        stage('Deploy to Staging') {
            steps {
                echo "Run integration tests in the staging environment"
                // sh 'mvn verify -Pstaging'
            }
        }

        stage('Deploy to Production') {
            steps {
                echo "Deploy to production using Ansible or other tools"
                // sh 'ansible-playbook -i inventory/production deploy.yml'
            }
        }
    }

    post {
        always {
            // Archive artifacts
            archiveArtifacts artifacts: '**', allowEmptyArchive: true
        }
    }
}
