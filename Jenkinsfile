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

                    sh './gradlew :test --tests "acceptation.DeterminantCalculatorFeature"'
                }
            }
            post {
                always {
                    junit 'build/test-results/test/*.xml'
                    cucumber 'build/reports/cucumber/*.json'
                }
            }
        }
    }
}