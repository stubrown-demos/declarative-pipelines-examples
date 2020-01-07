#!/usr/bin/env groovy
@Library("jenkins-shared-library") _

currentBuild.displayName = "#" + currentBuild.number + " - " + env.BRANCH_NAME

if (env.BRANCH_NAME == "master") {
    env.ENV_SUFFIX = ""
} else {
    env.ENV_SUFFIX = ".qa"
}

env.IMAGE_VERSION = env.BRANCH_NAME.replaceAll("/", ".").replaceAll("-", ".") + ".${BUILD_NUMBER}" + env.ENV_SUFFIX
env.DOCKER_IMAGE = "stuartcbrown/nginxtest:${IMAGE_VERSION}"

properties([buildDiscarder(logRotator(numToKeepStr: '10', artifactNumToKeepStr: '10'))])

pipeline {
    agent {
        kubernetes {
            label 'my-pod-template'
            defaultContainer 'jnlp'
            yaml """
apiVersion: v1
kind: Pod
metadata:
  labels:
    some-label: some-label-value
spec:
  containers:
  - name: docker
    image: docker:18.06
    command: ["cat"]
    tty: true
    volumeMounts:
    - mountPath: /var/run/docker.sock
      name: docker-socket
  volumes:
  - name: docker-socket
    hostPath:
      path: /var/run/docker.sock
      type: Socket
        
"""
        }
    }
    stages {
        stage('docker') {
            steps {
                container('docker') {
                    dockerLogin()
                    sh 'echo build_image'
                    sh "docker image build -t ${DOCKER_IMAGE} ."
                    sh 'docker images'
                    sh 'docker version'                    
                 
                   // sh "docker run -p 8032:90 ${DOCKER_IMAGE}"
                }
            }
        }
        stage('test') {
            steps {
                container('docker') {
                    sh "echo trying to start docker image ${DOCKER_IMAGE}"
                    sh "docker run  ${DOCKER_IMAGE}"
                    sh 'netstat -nlp'
                }
            }
        }
    }
    post {
        success {
            container('docker') {
                sh "docker push ${DOCKER_IMAGE}"
            }
        }
        failure {
            container('docker') {
                //sh "docker rmi ${DOCKER_IMAGE}"
            }
        }
    }
}
