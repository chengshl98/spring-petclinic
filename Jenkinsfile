pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        sh 'cd spring-petclinic'
        sh './mvnw package'
      }
    }
    stage('Sonarqube') {
        environment {
            scannerHome = tool 'SonarQubeScanner'
        }
        steps {
            withSonarQubeEnv('sonarqube') {
                sh "${scannerHome}/bin/sonar-scanner"
            }
            timeout(time: 10, unit: 'MINUTES') {
                waitForQualityGate abortPipeline: true
            }
        }
    }
  }
}
