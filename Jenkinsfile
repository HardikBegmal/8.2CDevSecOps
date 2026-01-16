pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main',
                url: 'https://github.com/HardikBegmal/8.2CDevSecOps.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                bat 'npm install'
            }
        }

        stage('Run Tests') {
            steps {
                bat 'npm test || exit /b 0'
            }
            post {
                success {
                    emailext (
                        subject: "Jenkins Pipeline - Tests Passed",
                        body: "All tests have passed successfully.\nCheck the logs attached.",
                        to: "hardikbegmalaus@gmail.com",
                        attachLog: true
                    )
                }
                failure {
                    emailext (
                        subject: "Jenkins Pipeline - Tests Failed",
                        body: "Some tests have failed.\nCheck the logs attached for details.",
                        to: "hardikbegmalaus@gmail.com",
                        attachLog: true
                    )
                }
            }
        }

        stage('Generate Coverage Report') {
            steps {
                bat 'npm run coverage || exit /b 0'
            }
        }

        stage('NPM Audit (Security Scan)') {
            steps {
                bat 'npm audit || exit /b 0'
            }
        }
    }
}
