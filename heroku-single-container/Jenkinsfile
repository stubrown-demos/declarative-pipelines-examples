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
  - name: heroku
    image: stuartcbrown/heroku-cli:latest
    command:
    - cat
    tty: true
"""
        }
    }
    stages {
        stage('Run maven') {
            steps {
                container('heroku') {
                    sh 'heroku clients'
                }
            }
        }
    }
}
