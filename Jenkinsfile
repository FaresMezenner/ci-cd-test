pipeline {
    agent any
    stages {

        stage('Hello') {
            steps {
                mail bcc: '', body: 'Test', subject: 'Test', to: 'faresmezenner@gmail.com'
            }
        }

        stage('Test') {
            steps {
                script {

                    sh './gradlew test --tests "acceptation.DeterminantCalculatorFeature"'
                    sh './gradlew test'
                }
            }
            post {
                always {
                    junit 'build/test-results/test/*.xml'
                    cucumber 'build/reports/cucumber/*.json'
                }
            }
        }
        stage('SonarQube') {
            steps {
                // Use the SonarQube environment wrapper
                withSonarQubeEnv('sonar') { // Replace 'SonarQube' with the name of your configured SonarQube server in Jenkins
                    sh './gradlew sonar '
                }
            }
        }

        stage('Code Quality') {
             steps {
                 script {
                     def qualityGate = waitForQualityGate() // Wait for SonarQube's analysis result
//                      if (qualityGate.status != 'OK') {
//                          error "Pipeline failed due to Quality Gate failure: ${qualityGate.status}"
//                      }
                 }
             }
         }
         stage('Build') {
             steps {
                 script {
                     // Generate the JAR file
                     sh './gradlew jar'

                     // Generate the documentation
                     sh './gradlew javadoc'
                 }
             }
             post {
                 success {
                     // Archive the generated JAR and documentation
                     archiveArtifacts artifacts: 'build/libs/*.jar', fingerprint: true
                     archiveArtifacts artifacts: 'build/docs/javadoc/**/*', fingerprint: true
                 }
             }
         }
             stage('Deploy') {
                 steps {
                     script {
                         sh './gradlew publish'
                     }
                 }
             }
    }
}