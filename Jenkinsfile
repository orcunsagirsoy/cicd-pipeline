pipeline {
  agent any
  stages {
    stage('Docker Manifest') {
      steps {
        script {
          checkout scm
          def customImage = docker.build("${registry}:${env.Build_ID}")
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

    stage('Build') {
      steps {
        script {
          docker.image("${registry}:${env.BUILD_ID}").inside{
            c-> sh '/scripts/build.sh'}
          }

        }
      }

      stage('Test') {
        steps {
          script {
            docker.image("${registry}:${env.BUILD_ID}").inside{
              c-> sh '/scripts/test.sh'}
            }

          }
        }

      }
      environment {
        registry = 'orcunsagirsoy/jenkinsapp'
      }
    }