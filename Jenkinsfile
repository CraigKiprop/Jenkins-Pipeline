pipeline {
    agent any

    environment {
        DIRECTORY_PATH = "C:/Users/craim/OneDrive/Desktop/code.html" //directory path
        TESTING_ENVIRONMENT = "Testing-environment" //name of your testing environment
        PRODUCTION_ENVIRONMENT = "Craig Kiprop Korir"
    }

    stages {
        stage('Build') {
            steps {
                echo "Fetch the source code from the directory path specified by C:/Users/craim/OneDrive/Desktop/code.html"
                echo "Compile the code and generate any necessary artifacts."
                // Add actual build steps here
            }
        }

        stage('Test') {
            steps {
                echo "Unit tests"
                echo "Integration tests"
                // Add actual test steps here
            }
        }

        stage('Code Quality Check') {
            steps {
                echo "Check the quality of the code."
                // Add actual code quality check steps here
            }
        }

        stage('Deploy') {
            steps {
                echo "Deploy the application to a testing environment (${env.TESTING_ENVIRONMENT})."
                // Add actual deployment steps here
            }
        }

        stage('Approval') {
            steps {
                sleep(time: 10, unit: 'SECONDS')
            }
        }

        stage('Deploy to Production') {
            steps {
                echo "Deploy the code to the production environment (${env.PRODUCTION_ENVIRONMENT})."
                // Add actual production deployment steps here
            }
        }
    }
}
