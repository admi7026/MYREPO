pipeline {
    agent any 

    stages {
        stage('Build') {
            steps {
                echo 'Stage 1: Build - Using Maven (example)'
                sh 'mvn clean package' 
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                echo 'Stage 2: Tests - Using JUnit, Mockito, etc. (examples)'
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
                // Integrate OWASP ZAP commands here:
                // 1. Start ZAP (if needed)
                // 2. Run the security scan
                // 3. Generate a report
            }
        }
        stage('Deploy to Staging') {
            steps {
                echo 'Stage 5: Deploy - Deploying to AWS EC2' 
                // Example using AWS CLI:
                sh 'aws deploy push --application-name MyApp --s3-location s3://my-bucket/deployment.zip --ignore-hidden-files'
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                echo 'Stage 6: Tests - Integration tests on staging'
                // Add your staging integration tests commands
            }
        }
        stage('Deploy to Production') {
            steps {
                echo 'Stage 7: Deploy - Deploying to AWS EC2'
                // Add your production deployment commands
            }
        }
    }

    post {
        always { 
            // Sent on both success and failure
            emailext body: 'Job ${env.JOB_NAME} build ${env.BUILD_NUMBER} finished - check console output at ${env.BUILD_URL}', 
                     to: 'your_email@example.com'
        }
        success {
            emailext body: 'Build Successful', to: 'your_email@example.com'
        }
        failure {
            emailext body: 'Build Failed - Check logs', to: 'your_email@example.com'
        }
    }
}
