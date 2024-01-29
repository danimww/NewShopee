pipeline {
  agent any
  tools {
    // Define the 'Maven' tool with the installation name 'Maven' (matches the tool configuration in Jenkins)
    maven 'Maven'
  }
  stages {
    stage('Build'){
      steps {
        // Use the 'withMaven' step to execute Maven build
        script {
          def mavenHome = tool 'Maven'
          withMaven(maven: mavenHome, mavenSettingsConfig: 'your-maven-settings-id') {
            sh 'mvn -B -DskipTests clean package'
          }
        }
      }
    }
    stage('Test'){
      steps {
        // Use the 'withMaven' step to execute Maven test
        script {
          def mavenHome = tool 'Maven'
          withMaven(maven: mavenHome, mavenSettingsConfig: 'your-maven-settings-id') {
            sh 'mvn test'
          }
        }
      }
      post {
        always {
          junit 'target/surefire-reports/*.xml'
        }
      }
    }
    stage('Deliver'){
      steps {
        // Use the 'withMaven' step to execute Maven and automatically set up the environment
        script {
          def mavenHome = tool 'Maven'
          withMaven(maven: mavenHome, mavenSettingsConfig: 'your-maven-settings-id') {
            sh './jenkins/scripts/deliver.sh'
          }
        }
      }
    }
  }
}
