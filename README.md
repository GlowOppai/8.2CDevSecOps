pipeline {
    agent any

    stages {

        stage('Build') {
            steps {
                echo 'Building code using Maven hehe'
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo 'Running tests using JUnit'
            }
        }

        stage('Code Analysis') {
            steps {
                echo 'Running code analysis using SonarQube'
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Scanning vulnerabilities using OWASP Dependency Check'
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to AWS EC2 staging server'
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo 'Running staging tests using Selenium'
            }
        }

        stage('Deploy to Production') {
            steps {
                echo 'Deploying to production server'
            }
        }
    }
}
