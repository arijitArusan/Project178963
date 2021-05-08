pipeline {
    agent any
    parameters {
    string (
        defaultValue: 'An error occurred (ValidationError) when calling the DescribeStacks operation: Stack with id S3Copy does not exist',
        description: '',
        name : 'STACK_CHECK')
    string (
        defaultValue: 'Y',
        description: '',
        name : 'STACK_CHECK2')
    }
    stages {
        stage('Check Stack Exists or Not') {
            steps {
            script{
            STACK_CHECK_RESULT=sh(
            script: "aws cloudformation describe-stacks --stack-name S3Coy --region us-east-1",
            returnStdout: true
           ).trim()
           echo "Status of Stack: ${STACK_CHECK_RESULT}"
           }
           }
        }
        stage('Create With out Delete') {
            when{
            expression{params.STACK_CHECK==${STACK_CHECK_RESULT}}
            }
            steps {
                echo "In Create without delete"

              }
             }
            }
            }
