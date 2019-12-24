pipeline {
    agent {
        kubernetes {
            label 'maven_build'
            defaultContainer 'jnlp'
            yaml """
apiVersion: v1
kind: Pod
metadata:
  labels:
    some-label: some-label-value
spec:
  containers:
  - name: maven
    image: maven:alpine
    command:
    - cat
    tty: true
"""
        }
    }
    stages {
        stage('Run maven build') {
            steps {
                container('maven'){
                    configFileProvider([configFile(fileId: '668c2e06-4ef5-4959-a613-91ef7644d46d', variable: 'MAVEN_SETTINGS_XML')]) {
                        sh "mvn -X -s $MAVEN_SETTINGS_XML deploy"
                    }
                }
            }    
        }
    }
}
