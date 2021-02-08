
pipeline {
    agent any
    stages {
        stage('Submit Stack') {
            steps {
            sh "aws cloudformation create-stack --stack-name vpc --template-body file://VPC.yml --region 'us-east-1'"
              }
             }
            }
            }
