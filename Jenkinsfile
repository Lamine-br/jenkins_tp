pipeline {
  agent any
  stages {
    stage ('test') {
      steps{
          bat 'gradle test'
          archiveArtifacts 'build/libs/*.jar'
      }
    }
    stage ('sonarQube') {
      steps{
          withSonarQubeEnv('SonarQube') {
              bat "gradle sonarqube"
          }
      }
    }
    stage("Quality gate") {
      steps {
          waitForQualityGate abortPipeline: true
      }
    }
  }
}
