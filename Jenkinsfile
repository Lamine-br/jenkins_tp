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
         bat "gradle sonarqube"
      }
    }
    stage("Quality gate") {
      steps {
          waitForQualityGate abortPipeline: true
      }
    }
  }
}
