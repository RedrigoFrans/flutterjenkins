pipeline {
    agent any

    environment {
        FLUTTER_HOME = '/home/redrigo/flutter'
        ANDROID_SDK_ROOT = '/home/redrigo/Android/Sdk'
        PATH = "${FLUTTER_HOME}/bin:${ANDROID_SDK_ROOT}/cmdline-tools/latest/bin:${ANDROID_SDK_ROOT}/platform-tools:${env.PATH}"
    }

    stages {
        stage('Build APK') {
            steps {
                dir('register_system/backend/flutter_app') {
                    sh '''
                        # Fix dubious ownership untuk Flutter SDK
                        git config --global --add safe.directory /home/redrigo/flutter
                        git config --global --add safe.directory ${WORKSPACE}

                        flutter clean
                        flutter pub get
                        flutter build apk --release
                    '''
                }
            }
        }

        stage('Archive APK') {
            steps {
                archiveArtifacts artifacts: '**/build/app/outputs/flutter-apk/*.apk',
                                 allowEmptyArchive: false
            }
        }
    }
}
