pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        sh './mvnw package'
      }
    }
    stage('Sonarqube Test') {
        environment {
            scannerHome = tool 'SonarQubeScanner'
        }
        steps {
          
            withSonarQubeEnv('sonar_server') {
                sh "${scannerHome}/bin/sonar-scanner "+
                    "-Dsonar.projectKey=petclinic " +
                    "-Dsonar.projectName=spring-petclinic " +
                    "-Dsonar.projectVersion=1.0.0 " +
                    "-Dsonar.java.binaries=/var/lib/jenkins/workspace/spring-petclinic_main/src " +
                    "-Dsonar.sourceEncoding=UTF-8"
            }
            timeout(time: 10, unit: 'MINUTES') {
                waitForQualityGate abortPipeline: true
            }
        }
    }
  }
}
