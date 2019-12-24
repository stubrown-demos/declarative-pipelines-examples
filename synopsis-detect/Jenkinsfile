pipeline{
    agent any
    stages{
        stage('build'){
            steps{
                echo 'building'

            }
        }
        stage('test and scan') {
            parallel {
                stage('test') {
                    steps {
                        echo 'testing'
                    }
                }
                stage('scan') {
                    steps {
                        sh "which java"
                        sh "env"
                        synopsys_detect '--detect.signature.scanner.host.url=https://sales.blackducksoftware.com --detect.signature.scanner.dry.run=true --blackduck.offline.mode=true'

                    }
                }
            }
        }
    
    }
    post{
            always{
                echo 'always'
            }
            success{
                echo 'success'
            }
            cleanup {
                echo 'cleaning up'
            }
        }
}
