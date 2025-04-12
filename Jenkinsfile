pipeline {
    agent any

    stages {
        stage('Testing Files') {
            steps {
                sh '''
                    echo "Wellcom to AWS Deploy WebSites"
                    test -f motivation/iindex.html
                '''
                
            }
        }
        stage('AWS Docker') {
           agent {
                  docker {
                    image 'amazon/aws-cli'
                    reuseNode true
                    args "--entrypoint=''"
                }           
           }

            environment {
                MY_BUCKET = 'learn-jenkins-david'
            }


           steps {
            withCredentials([usernamePassword(credentialsId: 'my-aws', passwordVariable: 'AWS_SECRET_ACCESS_KEY', usernameVariable: 'AWS_ACCESS_KEY_ID')]) {
                    // some block
                    sh '''
                    aws --version
                    aws s3 rm s3://$MY_BUCKET --recursive
                    aws s3 sync motivation s3://$MY_BUCKET
                    '''
           } 

            }
        }
    }
}
