pipeline {
  agent any
  stages {
    stage('') {
      steps {
        script {
          checkout scm
          def customImage = docker.build("${registry}:${env.Build_ID}")
        }

      }
    }

  }
  environment {
    registry = 'orcunsagirsoy/jenkinsapp'
  }
}