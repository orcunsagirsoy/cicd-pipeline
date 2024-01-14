pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        script {
          checkout scm
          def customImage = docker.build("${registry}:${env.Build_ID}")
        }

      }
    }

    stage('unit-test') {
      steps {
        script {
          docker.image("${registry}:${env.BUILD_ID}").inside{
            c-> sh 'chmod +x /scripts/build.sh | /scripts/build.sh'}
          }

        }
      }

      stage('Publish') {
        steps {
          script {
            docker.withRegistry('','docker_id'){
              docker.image("${registry}:${env.BUILD_ID}").push('latest')
              docker.image("${registry}:${env.BUILD_ID}").push("${env.BUILD_ID}")
            }
          }

        }
      }

    }
    environment {
      registry = 'orcunsagirsoy/jenkinsapp'
    }
  }