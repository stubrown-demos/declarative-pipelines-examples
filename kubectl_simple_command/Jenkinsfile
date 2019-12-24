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
  - name: k8s
    image: lachlanevenson/k8s-kubectl
    command:
    - cat
    tty: true
"""
        }
    }
    stages {
        stage('Run k8s') {
            steps {
                container('k8s') {
                    withCredentials([file(credentialsId: 'cli', variable: 'kubeconfig')]) {
                    //sh 'KUBECONFIG=$kubeconfig kubectl get pods --all-namespaces'
                    sh 'KUBECONFIG=$kubeconfig kubectl run nginx --image=nginx --replicas=1'
                    }
                }
                
            }
        }
    }
}
