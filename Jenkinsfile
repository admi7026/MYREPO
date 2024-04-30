pipeline {
    agent any 

    stages {
        stage('Build') {
            steps {
                echo 'Stage 1: Build - Using Maven (example)'
                sh 'mvn clean package' // If you use Maven 
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                echo 'Stage 2: Tests - Using JUnit, Mockito, etc. (examples)'
                sh 'mvn test' // Assuming Maven and JUnit
            }
        }
        stage('Code Analysis') {
            steps {
                echo 'Stage 3: Analysis - Using SonarQube'
                withSonarQubeEnv() { // Integrate SonarQube
                    sh 'mvn sonar:sonar' // Example Maven execution
                } 
            }
        }
        stage('Security Scan') {
            steps {
                echo 'Stage 4: Security Scan - Using OWASP ZAP'
                // Integrate OWASP ZAP security scan
            }
        }
        stage('Deploy to Staging') {
            steps {
                echo 'Stage 5: Deploy - Deploying to AWS EC2' 
                // Add your AWS deployment commands
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
                // Add production deployment commands
            }
        }
    }

    post {
        success {
            emailext body: 'Build Successful', to: 'hplapi62@gmail.com'
        }
        failure {
            emailext body: 'Build Failed - Check logs', to: 'hplapi62@gmail.com'
        }
    }
}
