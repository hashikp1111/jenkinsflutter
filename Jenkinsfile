pipeline {
    agent any

    environment {
        PATH = "/var/lib/jenkins/flutter/bin:${env.PATH}"
    }

    stages {
        stage('Check Flutter') {
            steps {
                sh 'flutter --version'
            }
        }

        stage('Get Dependencies') {
            steps {
                sh 'flutter pub get'
            }
        }

        stage('Analyze') {
            steps {
                sh 'flutter analyze'
            }
        }

        stage('Test') {
            steps {
                sh 'flutter test'
            }
        }

        stage('Build APK') {
            steps {
                sh 'flutter build apk --release'
            }
        }
    }

    post {
        success {
            archiveArtifacts(
                artifacts: 'build/app/outputs/flutter-apk/app-release.apk',
                fingerprint: true
            )
        }

        always {
            echo 'Jenkins pipeline finished.'
        }
    }
}