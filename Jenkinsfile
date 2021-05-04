pipeline {
    agent any
    stages {
        stage('Submit Stack') {
            steps {
            sh "aws cloudformation create-stack --stack-name S3Copy --template-body file://S3Copier.yml --parameters ParameterKey=REPO,ParameterValue=git://github.com/arijitArusan/Project178963 ParameterKey=VID,ParameterValue=178963 --region 'us-east-1'"
              }
             }
            }
            }