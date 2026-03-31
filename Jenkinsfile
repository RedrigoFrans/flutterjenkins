pipeline {
    agent any

    environment {
        FLUTTER_HOME     = '/home/redrigo/flutter'
        ANDROID_SDK_ROOT = '/home/redrigo/Android/Sdk'
        PATH             = "${FLUTTER_HOME}/bin:${ANDROID_SDK_ROOT}/cmdline-tools/latest/bin:${ANDROID_SDK_ROOT}/platform-tools:${env.PATH}"

        // ✅ Fix dubious ownership via environment variable (lebih reliable dari --global)
        GIT_CONFIG_COUNT   = '2'
        GIT_CONFIG_KEY_0   = 'safe.directory'
        GIT_CONFIG_VALUE_0 = '/home/redrigo/flutter'
        GIT_CONFIG_KEY_1   = 'safe.directory'
        GIT_CONFIG_VALUE_1 = '*'
    }

    stages {

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
        success { echo '✅ Build APK berhasil!' }
        failure { echo '❌ Build APK gagal. Cek log di atas.' }
    }
}
