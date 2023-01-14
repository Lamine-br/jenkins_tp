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
          bat 'gradle sonarQube'
      }
    }
    stage("Quality gate") {
      steps {
          waitForQualityGate abortPipeline: true
      }
    }
  }
}
