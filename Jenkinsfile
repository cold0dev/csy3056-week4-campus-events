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
        stage('Build Metadata') {
            steps {
                sh 'echo "Build number: $BUILD_NUMBER"  >  build-info.txt'
            }
        }
        stage('Archive Release') {
            steps {
                archiveArtifacts artifacts: 'dist/campus-events-1.1.0.zip, build-info.txt',
                                 fingerprint: true,
                                 allowEmptyArchive: false,
                                 onlyIfSuccessful: true
            }
        }
    }
}
