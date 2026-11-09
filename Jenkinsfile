pipeline {
    agent any

    environment {
        FLUTTER_HOME = 'C:\\Program Files\\flutter'
        GIT_HOME = 'D:\\Program\\Git\\cmd'
        POWERSHELL_HOME = 'C:\\Windows\\System32\\WindowsPowerShell\\v1.0'
        ANDROID_HOME = 'C:\\Users\\srypo\\AppData\\Local\\Android\\Sdk'
        JAVA_HOME = 'C:\\Program Files\\Eclipse Adoptium\\jdk-17.0.21.9-hotspot'
        
        PATH = "${JAVA_HOME}\\bin;${FLUTTER_HOME}\\bin;${GIT_HOME};C:\\Windows\\System32;${POWERSHELL_HOME};${ANDROID_HOME}\\cmdline-tools\\latest\\bin;${ANDROID_HOME}\\platform-tools;${env.PATH}"
    }

    stages {
        stage('Check Environment') {
            steps {
                bat 'git config --global --add safe.directory "*"'
                bat 'java -version'
                bat 'flutter --version'
            }
        }

        stage('Get Dependencies') {
            steps {
                echo 'Getting Flutter dependencies...'
                dir('flutter_application_hotelai') {
                    bat 'flutter pub get'
                }
            }
        }

        stage('Build APK') {
            steps {
                echo 'Building Android APK...'
                dir('flutter_application_hotelai') {
                    bat 'cd android && gradlew --stop'
                    bat 'flutter build apk --release'
                }
            }
        }
    }

    post {
        success {
            echo 'Build successful!'
        }
        failure {
            echo 'Build failed. Check log above.'
        }
    }
}