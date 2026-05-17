pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/GlowOppai/8.2CDevSecOps.git'
            }
        }
        
        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }
        
        stage('Run Tests') {
            steps {
                sh 'npm test || true'
            }
        }
        
        stage('Generate Coverage Report') {
            steps {
                sh 'npm run coverage || true'
            }
        }
        
        stage('NPM Audit (Security Scan)') {
            steps {
                sh 'npm audit || true'
            }
        }
    }
    
    post {
        always {
            emailext(
                subject: "Jenkins Build ${BUILD_NUMBER} - ${currentBuild.result}",
                body: """
                Build Number: ${BUILD_NUMBER}
                Build Status: ${currentBuild.result}
                Build URL: ${BUILD_URL}
                
                npm audit found security vulnerabilities.
                See attached logs for details.
                """,
                to: 'mallalamanmallalaman@gmail.com',
                attachLog: true
            )
        }
    }
}
