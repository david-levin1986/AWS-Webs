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
                
            withCredentials([usernamePassword(credentialsId: 'my-aws', passwordVariable: 'AWS_SECRET_ACCESS_KEY', usernameVariable: 'AWS_ACCESS_KEY_ID')]) {
                // some block
                sh '''
                aws --version
                
                '''
            }  
        }
    }
}
