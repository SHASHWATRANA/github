pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            when {
                branch 'main'
            }
            steps {
                echo 'Running full CI/CD pipeline for MAIN branch'
            }
        }

        stage('Test') {
            when {
                anyOf {
                    branch 'main'
                    branch 'feature/test-feature'
                    branch 'release/v1.0'
                }
            }
            steps {
                echo 'Running tests'
                bat 'python test.py'
            }
        }

        stage('Security Scan') {
            when {
                branch 'release/v1.0'
            }
            steps {
                echo 'Running security scans for RELEASE branch'
            }
        }
    }

    post {
        always {
            echo 'Pipeline completed'
        }
    }
}
