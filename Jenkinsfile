pipeline {
    agent any
    stages {


        stage('SonarQube') {
            steps {
                // Use the SonarQube environment wrapper
                withSonarQubeEnv('sonar') { // Replace 'SonarQube' with the name of your configured SonarQube server in Jenkins
                    sh './gradlew sonar '
                }
            }
        }

    }
    post {success {
                      // Email Notification for Successful Deployment
                      mail(
                          to: 'faresmezenner@gmail.com',
                          subject: 'Deployment Success - Project mezenner-ci-cd',
                          body: 'The deployment for the project mezenner-ci-cd was successful.'
                      )

                  }
                  failure {
                      // Email Notification for Pipeline Failure
                      mail(
                          to: 'faresmezenner@gmail.com',
                          subject: 'Pipeline Failed - Project mezenner-ci-cd',
                          body: 'The Jenkins pipeline for project mezenner-ci-cd has failed. Please check the logs for more details.'
                      )

                  }
    }
}