pipeline {
  agent any
  stages {
    stage ('Test') {
      steps{
          bat 'gradle test'
          archiveArtifacts 'build/libs/*.jar'
      }
    }
    stage ('Code Analysis') {
      steps{
        withSonarQubeEnv('sonar') {
          bat "gradle sonarqube"
        }
      }
    }
    stage("Code Quality") {
      steps {
          waitForQualityGate abortPipeline: true
      }
    }
  }
}
