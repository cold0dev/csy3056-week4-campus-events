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
	        steps { sh 'python3 scripts/build_release.py' }
	    }
        stage('Archive Release') {
            steps {
                archiveArtifacts artifacts: 'dist/campus-events-1.1.0.zip',
                                 fingerprint: true,
                                 allowEmptyArchive: false,
                                 onlyIfSuccessful: true
            }
        }
    }
}
