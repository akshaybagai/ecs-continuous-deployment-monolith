Steps

GIT_USER_NAME
GIT_TOKEN

- Forked https://github.com/akshaybagai/ecs-demo-php-simple-app
- Cloned https://github.com/awslabs/ecs-refarch-continuous-deployment - This has the cloud formation stack  
- Install AWS CLI
- Created AWS account and Configure CLI
    - Created IAM user
    - Update credentials in AWS CLI
        - aws configure
        - aws cloudformation create-stack --stack-name myteststack --template-body file:////Users/sa819de/labs/oneclickapi/cloudformationtests/s3bucket.yaml --parameters ParameterKey=TagName,ParameterValue=whateveriwant
        - aws cloudformation list-stacks
        - aws cloudformation delete-stack --stack-name testpipeline
        - aws cloudformation describe-stacks
        - aws s3api get-bucket-tagging --bucket myteststack-s3b3dz7w-uskvkad0wdoj
        - Update the stack
            aws cloudformation create-change-set --stack-name myteststack --change-set-name SampleChangeSet --template-body file:////Users/sa819de/labs/oneclickapi/cloudformationtests/s3bucket.yaml --parameters ParameterKey=TagName,ParameterValue=whateveriwanttodo
        - Describe change set
            aws cloudformation describe-change-set --change-set-name SampleChangeSet --stack-name myteststack
        - Execute changeset
            aws cloudformation execute-change-set --change-set-name SampleChangeSet --stack-name myteststack





aws cloudformation create-stack --stack-name testpipeline --capabilities CAPABILITY_IAM CAPABILITY_NAMED_IAM CAPABILITY_AUTO_EXPAND --template-body file://///Users/sa819de/labs/oneclickapi/ecs-refarch-continuous-deployment/ecs-refarch-continuous-deployment.yaml --parameters ParameterKey=GitHubUser,ParameterValue=GIT_USER_NAME ParameterKey=GitHubToken,ParameterValue=GIT_TOKEN
aws cloudformation create-change-set --change-set-name UpdatedGitParameter --stack-name testpipeline --capabilities CAPABILITY_IAM CAPABILITY_NAMED_IAM CAPABILITY_AUTO_EXPAND --template-body file://///Users/sa819de/labs/oneclickapi/ecs-refarch-continuous-deployment/ecs-refarch-continuous-deployment.yaml --parameters ParameterKey=GitHubUser,ParameterValue=GIT_USER_NAME ParameterKey=GitHubToken,ParameterValue=GIT_TOKEN
aws cloudformation describe-change-set --change-set-name UpdatedGitParameter --stack-name testpipeline
aws cloudformation execute-change-set --change-set-name UpdatedGitParameter --stack-name testpipeline
