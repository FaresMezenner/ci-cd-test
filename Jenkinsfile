pipeline {
    agent any
    stages {
//         stage('SonarQube') {
//             steps {
//                 sh './gradlew sonar'
//             }
//         }
        stage('test') {
            steps {
                echo 'Hello World 5'
            }
        }
        stage('Test') {
            steps {
                script {
                    sh './gradlew test'
                    junit 'build/test-results/**/*.xml'
                }
            }
        }
    }
}