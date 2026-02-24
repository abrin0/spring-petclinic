pipeline {
  agent any

  triggers { cron('H/5 * * * 1') }

  tools {
    maven 'Maven'
  }

  stages {
    stage('Checkout') { steps { checkout scm } }

    stage('Build and Test with JaCoCo') {
      steps { bat 'mvn -B clean test' }
    }

    stage('Generate JaCoCo Report') {
      steps { bat 'mvn -B jacoco:report' }
    }
  }

  post {
    always {
      archiveArtifacts artifacts: 'target/site/jacoco/**', allowEmptyArchive: true
      // make junit not fail the build if something went wrong earlier
      junit testResults: '**/target/surefire-reports/*.xml', allowEmptyResults: true
    }
  }
}