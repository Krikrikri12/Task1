pipeline {
    agent any
    environment {
        AWS_ACCESS_KEY_ID     = credentials('jenkins-aws-secret-key-id')
        AWS_SECRET_ACCESS_KEY = credentials('jenkins-aws-secret-access-key')
    }
    stages {
        stage('upload templates to S3') {
            steps {
                withAWS(region:'us-east-1') {
                    s3Upload(file:'VPC.yml', 
                            bucket:'templateofvpc')
                }
                withAWS(region:'us-east-1') {
                    s3Upload(file:'nginx-ecs.yml', 
                            bucket:'templateofvpc')
                }

         }
      }        
 
        stage('Submit VPC') {
            steps {
            sh "aws cloudformation create-stack --stack-name VPCStack --template-body file://VPC.yml --region 'us-east-1' --capabilities CAPABILITY_NAMED_IAM"
         }
      }
 
        stage('Submit Stack') {
            steps {
            sh "aws cloudformation create-stack --stack-name ECSCluster --template-body file://nginx-ecs.yml --region 'us-east-1' --capabilities CAPABILITY_NAMED_IAM"
         }
      }
   }     
    post {
        always {
            deleteDir()
      }
   }
}

