pipeline {
    agent any

    stages {
        stage('Testing Files') {
            steps {
                sh '''
                    echo "Wellcom to AWS Deploy WebSites"
                    test -f motivation/index.html
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
                    echo "Starting Uplode WebSite to AWS"
                    aws s3 rm s3://$MY_BUCKET --recursive
                    aws s3 sync motivation s3://$MY_BUCKET
                    echo "Starting WebSite Testing"
                    aws s3 ls s3:////$MY_BUCKET/index.html || { echo "Index.html nut exist the WebSite Deployment Faild"; exit 1; }
                    curl -s https://$MY_BUCKET/index.html | grep "Welcome to my website" || { echo "Error The Index Not Fund in the WebSite"; exit 1; }
                    '''
           } 

            }
        }
    }
}
