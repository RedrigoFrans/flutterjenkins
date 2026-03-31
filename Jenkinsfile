pipeline {
    agent any

    environment {
        PATH = "/home/redrigo/flutter/bin:$PATH"
        ANDROID_HOME = "/home/redrigo/Android/Sdk"
    }

    stages {
        stage('Build APK') {
            steps {
                dir('register_system/backend/flutter_app') {
                    // --- Tambahkan baris ini untuk memberikan izin keamanan Git ---
                    sh 'git config --global --add safe.directory /home/redrigo/flutter'
                    
                    sh 'flutter clean'
                    sh 'flutter pub get'
                    sh 'flutter build apk --release'
                }
            }
        }
        
        stage('Archive APK') {
            steps {
                archiveArtifacts artifacts: 'register_system/backend/flutter_app/build/app/outputs/flutter-apk/app-release.apk', allowEmptyArchive: true
            }
        }
    }
}
