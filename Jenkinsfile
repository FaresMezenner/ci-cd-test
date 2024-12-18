pipeline {
    agent any
    stages {
        stage('SonarQube') {
            sh './gradlew sonar'
        }
        stage('test') {
            steps {
                echo 'Hello World 5'
            }
        }
    }
}