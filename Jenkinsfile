pipeline {
    agent any

    // Memberitahu Jenkins lokasi Flutter dan Android SDK milikmu
    environment {
        PATH = "/home/redrigo/flutter/bin:$PATH"
        ANDROID_HOME = "/home/redrigo/Android/Sdk"
    }

    stages {
        stage('Build APK') {
            steps {
                dir('register_system/backend/flutter_app') {
                    sh 'flutter clean'
                    sh 'flutter pub get'
                    sh 'flutter build apk --release'
                }
            }
        }
        
        // Opsional: Menyimpan hasil APK agar bisa di-download langsung dari Jenkins
        stage('Archive APK') {
            steps {
                archiveArtifacts artifacts: 'register_system/backend/flutter_app/build/app/outputs/flutter-apk/app-release.apk', allowEmptyArchive: true
            }
        }
    }
}
