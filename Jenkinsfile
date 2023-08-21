pipeline {
    agent any
    
    stages {
        stage('Build') {
            steps {
                // Define build steps here
                sh 'mvn clean package'
            }
        }
        
        stage('Unit Tests') {
            steps {
                // Define unit test steps here
                sh 'mvn test'
            }
        }
        
        // Define other stages similarly
        
        // ...
    }
    
    post {
        always {
            mail to: "craigkorir@gmail.com",
                subject: "Build Status",
                body: "Build log"
            // Define post-build actions here
            // For example, archiving artifacts and sending email notifications
        }
    }
}
