pipeline {
    agent any

    stages {
        stage('Wellcom') {
            steps {
                echo 'Wellcom to AWS Web Deploy Tool'
            }
        }
        stage('AWS Docker') {
           agent {
                docker {
                    image 'amazon/aws-cli'
                    args "--entrypoint''"
                }            
           }

           steps {
            sh '''
            aws --version
            '''
           } 

        }
    }
}
