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
    }
}
