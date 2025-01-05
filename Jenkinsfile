pipeline {
    agent any
    stages {


//         stage('Test') {
//             steps {
//                 script {
//
//                     sh './gradlew test --tests "acceptation.DeterminantCalculatorFeature"'
//                     sh './gradlew test'
//                 }
//             }
//             post {
//                 always {
//                     junit 'build/test-results/test/*.xml'
//                     cucumber 'build/reports/cucumber/*.json'
//                 }
//             }
//         }

        stage('SonarQube') {
            steps {
                // Use the SonarQube environment wrapper
                withSonarQubeEnv('sonar') { // Replace 'SonarQube' with the name of your configured SonarQube server in Jenkins
                    sh './gradlew sonar '
                }
            }
        }

//         stage('Code Quality') {
//              steps {
//                  script {
//                      def qualityGate = waitForQualityGate() // Wait for SonarQube's analysis result
// //                      if (qualityGate.status != 'OK') {
// //                          error "Pipeline failed due to Quality Gate failure: ${qualityGate.status}"
// //                      }
//                  }
//              }
//          }
//          stage('Build') {
//              steps {
//                  script {
//                      // Generate the JAR file
//                      sh './gradlew jar'
//
//                      // Generate the documentation
//                      sh './gradlew javadoc'
//                  }
//              }
//              post {
//                  success {
//                      // Archive the generated JAR and documentation
//                      archiveArtifacts artifacts: 'build/libs/*.jar', fingerprint: true
//                      archiveArtifacts artifacts: 'build/docs/javadoc/**/*', fingerprint: true
//                  }
//              }
//          }
//              stage('Deploy') {
//                  steps {
//                      script {
//                          sh './gradlew publish'
//                      }
//                  }
//              }
    }
    post {success {
                      // Email Notification for Successful Deployment
                      mail(
                          to: 'faresmezenner@gmail.com',
                          subject: 'Deployment Success - Project mezenner-ci-cd',
                          body: 'The deployment for the project mezenner-ci-cd was successful.',
                          attachLog: true
                      )

                      // Slack Notification for Successful Deployment
//                       slackSend(
//                           channel: '#development',
//                           color: 'good',
//                           message: 'Deployment succeeded for project mezenner-ci-cd!'
//                       )
                  }
                  failure {
                      // Email Notification for Pipeline Failure
                      mail(
                          to: 'faresmezenner@gmail.com',
                          subject: 'Pipeline Failed - Project mezenner-ci-cd',
                          body: 'The Jenkins pipeline for project mezenner-ci-cd has failed. Please check the logs for more details.',
                          attachLog: true
                      )

                      // Slack Notification for Pipeline Failure
//                       slackSend(
//                           channel: '#development',
//                           color: 'danger',
//                           message: 'Pipeline failed for project mezenner-ci-cd. Check Jenkins for details!'
//                       )
                  }
    }
}