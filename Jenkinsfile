pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        sh './mvnw package'
        sh 'export job=$job:spring-petclinic'
      }
    }
    stage('Sonarqube Test') {
        environment {
            scannerHome = tool 'SonarQubeScanner'
        }
        steps {
          
            withSonarQubeEnv('sonar_server') {
                sh "${scannerHome}/bin/sonar-scanner"
            }
            timeout(time: 10, unit: 'MINUTES') {
                waitForQualityGate abortPipeline: true
            }
        }
    }
  }
}
