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
                        withCoverityEnv(coverityToolName: '', hostVariable: '', passwordVariable: '', portVariable: '', usernameVariable: '') {
                         echo 'scanning'
                         }
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
