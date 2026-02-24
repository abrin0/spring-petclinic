pipeline {
  agent any

  triggers {
    cron('H/5 * * * 1')
  }

  options {
    timestamps()
  }

  stages {

    stage('Checkout') {
      steps {
        checkout scm
      }
    }

    stage('Build and Test with JaCoCo') {
      steps {
        bat 'mvn clean test'
      }
    }

    stage('Generate JaCoCo Report') {
      steps {
        bat 'mvn jacoco:report'
      }
    }
  }

  post {
    always {
      archiveArtifacts artifacts: 'target/site/jacoco/**', allowEmptyArchive: true
      junit '**/target/surefire-reports/*.xml'
    }
  }
}