pipeline {
    agent any
    parameters {
    string (
        defaultValue: 'N',
        description: '',
        name : 'STACK_CHECK')
    }
    stages {
        stage('Check Stack Exists or Not') {
            steps {
            script{
            STACK_CHECK_RESULT="STACK_CHECK_RESULT"
            }
            STACK_CHECK_RESULT=sh(
            script: "aws cloudformation describe-stacks --stack-name S3Copy",
            returnStdout: true
           ).trim()
           echo "Status of Stack: ${STACK_CHECK_RESULT}"
           }
        }
        stage('Submit Stack') {
            steps {
            sh "aws cloudformation create-stack --stack-name S3Copy --template-body file://S3Copier.yml --parameters ParameterKey=REPO,ParameterValue=git://github.com/arijitArusan/Project178963 ParameterKey=VID,ParameterValue=178963 --region 'us-east-1'"
              }
             }
            }
            }