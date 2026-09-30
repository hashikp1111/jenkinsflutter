pipeline {
    agent any

    environment {
        ANDROID_HOME = '/opt/android-sdk'
        PATH = "/var/lib/jenkins/flutter/bin:/opt/android-sdk/platform-tools:/opt/android-sdk/cmdline-tools/latest/bin:${env.PATH}"
    }

    stages {
        stage('Check Flutter and Android SDK') {
            steps {
                sh 'flutter --version'
                sh 'flutter doctor --verbose'
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