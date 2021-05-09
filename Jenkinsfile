def getstatus(){
    try{
    STACK_CHECK_RESULT=sh(
            script: "aws cloudformation describe-stacks --stack-name S3Copy --region us-east-1",
            returnStatus:true
           )
    } catch (Exception e){
      echo 'Exception occurred: ' + e.toString()
    }finally{
      return STACK_CHECK_RESULT
      }

}
pipeline {
    agent any
    environment {
    STACK_CHECK_RESULT = getstatus()
  }

    stages {
        stage('Check Stack Exists or Not') {
            steps {
            echo "${STACK_CHECK_RESULT}"
           }
        }
        stage('Create With Delete') {
            when{
            expression{"${STACK_CHECK_RESULT}"=="0"}
            }
            steps {
                echo "The Stack Already Exist"
                echo "Started Deleting Stack"
                sh "aws cloudformation delete-stack --stack-name S3Copy --region us-east-1"
                sleep(time:20,unit:"SECONDS")
                echo "Stack Deleted"
                echo "Started Creating Stack"
                sh "aws cloudformation create-stack --stack-name S3Copy --template-body file://S3Copier.yml --parameters ParameterKey=REPO,ParameterValue=git://github.com/arijitArusan/Project178963 ParameterKey=VID,ParameterValue=178963 --region 'us-east-1'"
                echo "Job Created"
              }
             }
        stage('Create Without Delete') {
            when{
            expression{"${STACK_CHECK_RESULT}"=="255"}
            }
            steps {
                echo "Started Creating Stack"
                sh "aws cloudformation create-stack --stack-name S3Copy --template-body file://S3Copier.yml --parameters ParameterKey=REPO,ParameterValue=git://github.com/arijitArusan/Project178963 ParameterKey=VID,ParameterValue=178963 --region 'us-east-1'"
                echo "Job Created"
              }
             }
            }
            }
