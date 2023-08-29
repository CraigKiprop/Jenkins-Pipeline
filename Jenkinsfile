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
                
                // Create a ZIP file using Windows command (bat)
                bat 'del test.zip'
                bat 'echo. > empty.txt'
                bat 'powershell Compress-Archive -Path empty.txt -DestinationPath test.zip'
            }
        }

        // ... other stages ...

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
                def attachmentsPattern = '**/*.log'
                
                // Create an empty file named 'empty.txt'
                def emptyFile = new File("${env.WORKSPACE}/empty.txt")
                emptyFile.createNewFile()
                
                // Attach the ZIP file
                emailext subject: "Integration Test Status",
                         body: "Integration test logs attached",
                         mimeType: 'text/plain',
                         to: "craigkorir@gmail.com",
                         attachmentsPattern: attachmentsPattern,
                         attachments: "test.zip"
            }
        }
    }
}
