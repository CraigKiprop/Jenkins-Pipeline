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
                //sh 'mvn test'
                // Add actual test steps here
                archiveArtifacts artifacts: '**/*.log', allowEmptyArchive: true
                
                // Create an empty file named 'empty.txt'
                writeFile file: 'empty.txt', text: ''
                zip zipFile: 'test.zip', archive: false, dir: '.'
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
                // sh 'zap-cli --spider <your_app_url>'
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
            script {
                // Define the attachmentsPattern
                def attachmentsPattern = '**/*.log'
                
                // Create an empty file named 'empty.txt'
                def emptyFile = new File("${env.WORKSPACE}/empty.txt")
                emptyFile.createNewFile()
                
                emailext subject: "Integration Test Status",
                         body: "Integration test logs attached",
                         mimeType: 'text/plain',
                         to: "craigkorir@gmail.com",
                         attachmentsPattern: attachmentsPattern,
                         presendScript: """
                             msg.addAttachment(emptyFile)
                         """
            }
        }
    }
}
