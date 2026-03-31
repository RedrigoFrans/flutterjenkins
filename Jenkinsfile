pipeline {
    agent any

    environment {
        FLUTTER_HOME    = '/home/redrigo/flutter'
        ANDROID_SDK_ROOT = '/home/redrigo/Android/Sdk'
        PATH            = "${FLUTTER_HOME}/bin:${ANDROID_SDK_ROOT}/cmdline-tools/latest/bin:${ANDROID_SDK_ROOT}/platform-tools:${env.PATH}"
    }

    stages {

        stage('Fix Git Ownership') {
            steps {
                sh '''
                    git config --global --add safe.directory /home/redrigo/flutter
                    git config --global --add safe.directory ${WORKSPACE}
                '''
            }
        }

        stage('Build APK') {
            steps {
                dir('register_system/backend/flutter_app') {
                    sh '''
                        flutter clean
                        flutter pub get
                        flutter build apk --release
                    '''
                }
            }
        }

        stage('Archive APK') {
            steps {
                archiveArtifacts(
                    artifacts: '**/build/app/outputs/flutter-apk/*.apk',
                    allowEmptyArchive: false
                )
            }
        }

    }

    post {
        success {
            echo '✅ Build APK berhasil!'
        }
        failure {
            echo '❌ Build APK gagal. Cek log di atas.'
        }
    }
}
