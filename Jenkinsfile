pipeline {
    agent any 

    stages {
        stage('Build') {
            steps {
                echo 'Stage 1: Build - Using Maven'
                sh 'mvn clean package' 
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                echo 'Stage 2: Tests - Using JUnit, Mockito'
                sh 'mvn test' 
            }
        }
        stage('Code Analysis') {
            steps {
                echo 'Stage 3: Analysis - Using SonarQube'
                withSonarQubeEnv() { 
                    sh 'mvn sonar:sonar' 
                } 
            }
        }
        stage('Security Scan') {
            steps {
                echo 'Stage 4: Security Scan - Using OWASP ZAP'
                sh 'zap-cli --start'
                sh 'zap-cli --quick-scan --self-contained --spider <target_url>'
                sh 'zap-cli --report'
            }
        }
        stage('Deploy to Staging') {
            steps {
                echo 'Stage 5: Deploy - Deploying to AWS EC2' 
                sh 'aws deploy push --application-name MyApp --s3-location s3://my-bucket/deployment.zip --ignore-hidden-files'
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                echo 'Stage 6: Tests - Integration tests on staging'
                sh 'run_integration_tests.sh staging'
            }
        }
        stage('Deploy to Production') {
            steps {
                echo 'Stage 7: Deploy - Deploying to AWS EC2'
                sh 'deploy_to_production.sh'
            }
        }
    }

    post {
        always { 
            // Sent on both success and failure
            emailext subject: "Build Status Notification",
                     body: "Job ${env.JOB_NAME} build ${env.BUILD_NUMBER} finished - check console output at ${env.BUILD_URL}",
                     to: 'your_email@example.com'
        }
        success {
            emailext subject: "Build Successful",
                     body: "Build Successful",
                     to: 'your_email@example.com'
        }
        failure {
            emailext subject: "Build Failed",
                     body: "Build Failed - Check logs",
                     to: 'your_email@example.com'
        }
    }
}
