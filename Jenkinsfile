pipeline{
  agent any
  stages{
    stage("Build"){
      steps{
        bat 'printenv'
        
      }
    }
    stage ('Publish ECR'){
      steps{
        withEnv(["AWS_ACCESS_KEY_ID=$(env.AWS_ACCESS_KEY_ID)","AWS_SECRET_ACCESS_KEY=$(env.AWS_SECRET_ACCESS_KEY)","AWS_DEFAULT_REGION=$(env.AWS_DEFAULT_REGION)"]){
          bat 'docker login -u AWS -p $(aws ecr-public get-login-password --region us-east-1) public.ecr.aws/g9t7d5z8'
          bat 'docker build -t dockerdemo .'
          bat 'docker tag dockerdemo:latest public.ecr.aws/g9t7d5z8/dockerdemo:""$BUILD_ID""'
          bat 'docker push public.ecr.aws/g9t7d5z8/dockerdemo:""$BUILD_ID""'
        }
      }
    }
  }
}
