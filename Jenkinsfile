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

    stage('Build') {
      steps {
        script {
          docker.image("${registry}:${env.BUILD_ID}").inside{
            c-> sh 'cd scripts && chmod +x build.sh && ./build.sh'}
          }
        }
      }

      stage('Test') {
        steps {
          script {
            docker.image("${registry}:${env.BUILD_ID}").inside{
              c-> sh 'cd scripts && chmod +x test.sh && ./test.sh'}
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
