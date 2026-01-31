pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                echo 'Checking out source code'
                checkout scm
            }
        }

        stage('Build') {
            when {
                branch 'main'
            }
            steps {
                echo 'Running build on MAIN branch'
                bat 'echo Build completed'
            }
        }

        stage('Test') {
            when {
                anyOf {
                    branch 'main'
                    branch 'feature/test-feature'
                }
            }
            steps {
                echo 'Running tests'
                bat '"C:\\Users\\shash\\AppData\\Local\\Programs\\Python\\Python314\\python.exe" --version'
                bat '"C:\\Users\\shash\\AppData\\Local\\Programs\\Python\\Python314\\python.exe" test.py'
            }
        }

        stage('Security Scan') {
            when {
                branch 'release/v1.0'
            }
            steps {
                echo 'Running security scan for RELEASE branch'
                bat 'echo Security scan completed'
            }
        }
    }

    post {
        always {
            echo 'Pipeline execution finished'
        }
        success {
            echo 'Pipeline succeeded'
        }
        failure {
            echo 'Pipeline failed'
        }
    }
}

