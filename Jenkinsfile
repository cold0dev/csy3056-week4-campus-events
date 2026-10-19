pipeline {
    agent any
    options { skipDefaultCheckout(true) }
    stages {
        stage('Checkout') {
            steps { checkout scm }
        }
        stage('Setup') {
            steps { sh 'python3 --version' }
        }
        stage('Validate Application') {
            steps { sh 'python3 scripts/check_app.py' }
        }
        stage('Package Release') {
            steps { sh 'python3 scripts/build_releases.py' }
        }
        stage('Archive Release') {
            steps { archiveArtifacts artifacts: 'dist/*.zip', fingerprint: true }
        }
        stage('Build Metadata') {
            steps {
                bat 'echo Build Number: %BUILD_NUMBER% > build-info.txt'
                archiveArtifacts artifacts: 'build-info.txt'
            }
        }
    }
}
