pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building the code...'
                // Example: sh 'mvn clean package'
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                echo 'Running unit and integration tests...'
                // Example: sh 'mvn test'
            }
        }
        stage('Code Analysis') {
            steps {
                echo 'Performing code analysis...'
                // Example: sh 'sonar-scanner'
            }
        }
        stage('Security Scan') {
            steps {
                echo 'Running security scan...'
                // Example: sh 'dependency-check'
            }
        }
        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to staging environment...'
                // Example: sh 'scp target/myapp.jar user@staging-server:/deployments'
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                echo 'Running integration tests on staging...'
                // Example: sh 'mvn verify -Pstaging'
            }
        }
        stage('Deploy to Production') {
            steps {
                echo 'Deploying to production environment...'
                // Example: sh 'scp target/myapp.jar user@production-server:/deployments'
            }
        }
    }
    post {
        success {
            emailext (
                subject: "Jenkins Pipeline Success: ${env.JOB_NAME} [${env.BUILD_NUMBER}]",
                body: """Success: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]' succeeded.
                Check console output at ${env.BUILD_URL}""",
                to: 'maddilaharshith@gmail.com'
            )
        }
        failure {
            emailext (
                subject: "Jenkins Pipeline Failure: ${env.JOB_NAME} [${env.BUILD_NUMBER}]",
                body: """Failure: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]' failed.
                Check console output at ${env.BUILD_URL}""",
                to: 'maddilaharshith@gmail.com'
            )
        }
    }
}
