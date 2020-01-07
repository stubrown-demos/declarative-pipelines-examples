def label1 = "pl_scripted_docker_dind-${UUID.randomUUID().toString()}"
pipeline {
  agent {
    kubernetes {
      //cloud 'kubernetes'
      label 'pl_scripted_docker_dind'
      containerTemplate {
        name 'maven'
        image 'maven:3.3.9-jdk-8-alpine'
        ttyEnabled true
        command 'cat'
      }
    }
  }
  stages {
    stage('Run maven') {
      steps {
        container('maven') {
          sh 'mvn -version'
          sh 'docker -version'
        }
      }
    }
  }
}
