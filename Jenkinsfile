pipeline {
    agent any 

    stages {
        stage('Build') {
            steps {
                echo 'Stage 1: Build - Using Maven (example)'
                // Add your actual build commands here (e.g., 'mvn package')
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                echo 'Stage 2: Tests - Using JUnit, Mockito, etc. (examples)'
                // Add your testing commands here (e.g., 'mvn test')
            }
        }
        stage('Code Analysis') {
            steps {
                echo 'Stage 3: Analysis - Using SonarQube (example)'
                // Add SonarQube integration here (e.g., withSonarQubeEnv() {})
            }
        }
        stage('Security Scan') {
            steps {
                echo 'Stage 4: Security - Using OWASP ZAP (example)'
                // Add OWASP ZAP integration here
            }
        }
        stage('Deploy to Staging') {
            steps {
                echo 'Stage 5: Deploy - Deploying to AWS EC2'
                // Add your AWS deployment commands here 
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                echo 'Stage 6: Tests - Integration tests on staging'
                // Add staging tests here
            }
        }
        stage('Deploy to Production') {
            steps {
                echo 'Stage 7: Deploy - Deploying to AWS EC2'
                // Add your production deployment commands here
            }
        }
    }

    post {
        always { 
            // Sent on both success and failure
            emailext body: 'Job ${env.JOB_NAME} build ${env.BUILD_NUMBER} finished - check console output at ${env.BUILD_URL}', 
                     to: 'hplapi62@gmail.com'
        }
        success {
            emailext body: 'Build Successful', to: 'hplapi62@gmail.com'
        }
        failure {
            emailext body: 'Build Failed - Check logs', to: 'hplapi62@gmail.com'
        }
    }
}
