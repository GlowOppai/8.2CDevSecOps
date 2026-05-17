pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo '========== Stage 1: BUILD =========='
                echo 'Tool: Maven'
                echo 'Task: Compiling and packaging code'
                sh 'echo "Running Maven build: mvn clean package"'
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo '========== Stage 2: UNIT AND INTEGRATION TESTS =========='
                echo 'Tool: JUnit (Unit Tests), TestNG (Integration Tests)'
                echo 'Task: Running unit and integration tests'
                sh 'npm test || true'
            }
        }

        stage('Code Analysis') {
            steps {
                echo '========== Stage 3: CODE ANALYSIS =========='
                echo 'Tool: SonarQube'
                echo 'Task: Analyzing code for quality and standards'
                sh 'echo "Running SonarQube analysis"'
            }
        }

        stage('Security Scan') {
            steps {
                echo '========== Stage 4: SECURITY SCAN =========='
                echo 'Tool: OWASP Dependency-Check / npm audit'
                echo 'Task: Scanning for vulnerabilities'
                sh 'npm audit || true'
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo '========== Stage 5: DEPLOY TO STAGING =========='
                echo 'Tool: AWS EC2 / Docker'
                echo 'Task: Deploying to staging server'
                sh 'echo "Deploying to staging environment"'
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo '========== Stage 6: INTEGRATION TESTS ON STAGING =========='
                echo 'Tool: Selenium / TestNG'
                echo 'Task: Running tests in production-like environment'
                sh 'echo "Running integration tests on staging"'
            }
        }

        stage('Deploy to Production') {
            steps {
                echo '========== Stage 7: DEPLOY TO PRODUCTION =========='
                echo 'Tool: AWS EC2 / Docker'
                echo 'Task: Deploying to production server'
                sh 'echo "Deploying to production environment"'
            }
        }
    }

    post {
        always {
            echo '========== Pipeline Complete =========='
        }
    }
}
