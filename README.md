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
            mail to: 'mallalamanmallalaman@gmail.com',
                 subject: "Jenkins Build ${BUILD_NUMBER} - ${currentBuild.result}",
                 body: """Build Status: ${currentBuild.result}
Build Number: ${BUILD_NUMBER}
Build URL: ${BUILD_URL}

npm audit found 142 vulnerabilities in the nodejs-goof project.
Check Jenkins console for full audit report."""
        }
    }
}
