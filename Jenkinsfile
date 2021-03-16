pipeline {
    agent any
    environment {
        AWS_ACCESS_KEY_ID     = credentials('jenkins-aws-secret-key-id')
        AWS_SECRET_ACCESS_KEY = credentials('jenkins-aws-secret-access-key')
    }
    stages {
        stage('Submit VPC') {
            steps {
            sh "aws cloudformation create-stack --stack-name vpc4 --template-body file://VPC.yml --region 'us-east-1' --capabilities CAPABILITY_NAMED_IAM"
         }
      }
   } 
    stages {
        stage('Submit Stack') {
            steps {
            sh "aws cloudformation create-stack --stack-name vpc4 --template-body file://nginx-ecs.yml --region 'us-east-1' --capabilities CAPABILITY_NAMED_IAM"
         }
      }
   }     
    post {
        always {
            deleteDir()
      }
   }
}

