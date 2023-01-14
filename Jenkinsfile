pipeline {
  agent any
  stages {
    stage ('test') {
      steps{
          bat 'gradle test'
      }
    }
    stage ('build') {
      steps{
          bat 'gradle build'
          archiveArtifacts 'build/libs/*.jar'
      }
    }
  }
}
