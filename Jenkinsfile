pipeline {
  agent any
  stages {
    stage ('Test') {
      steps{
          bat 'gradle test'
          cucumber buildStatus: 'UNSTABLE',
                reportTitle: 'Report',
                fileIncludePattern: '*/.json',
                trendsLimit: 10
          junit 'build/test-results/test/TEST-Matrix.xml'
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
    stage("Build") {
      steps {
          bat "gradle build"
          bat "gradle javadoc"
          archiveArtifacts 'build/libs/*.jar'
          archiveArtifacts 'build/docs/'
      }
    }
    stage("Deploy") {
      steps {
          bat "gradle publish" 
      } 
    }  
    stage("Notification") {
      steps {
          notifyEvents message: 'Bonsoir <b>mon ami</b>', token: 'Vmg23LVKMDqFBR19m2ttgrSHRSbzDU_K'
      }
    }
  }
}
