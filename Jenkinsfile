pipeline {
    agent any
 
    stages {
        stage('checkout') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/Shi191099/Android_app.git']]])
            }
        }
        stage('gradle clean'){
            steps {
                sh './gradlew clean'
            }
        }
        stage('build gradlew') {
            steps {
                sh './gradlew assembleRelease'
            }
        }
         stage('apk file') {
            steps {
                archiveArtifacts artifacts: '**/*.apk', fingerprint: true, onlyIfSuccessful: true
            }
        }
        stage('Artifacte upload') {
            steps {
                echo 'Hello'
                appCenter apiToken: '34cfa992bf0cf31a60c78c42e7c15a8b00e045f1', 
                appName: 'Android-Poc', 
                distributionGroups: 'android-apk-1', 
                mandatoryUpdate: false, 
                notifyTesters: true, 
                ownerName: 'shital191099-gmail.com', 
                pathToApp: '**/*.apk'
            }
        }
    }
}
