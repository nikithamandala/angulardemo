pipeline{
  agent any
  stages{
    stage ('checkout'){
      steps{
        checkout scm
      }
    }
   stage ('Build'){
       parallel {
             stage("Angular Build") {
                  agent {
                      docker { image 'node:10' }
                  }
                  steps {
                         echo Installing packages
                         npm install
                         npm install -g @angular/cli@8
                         echo Building Angular Project
                         ng build
                  }
             }
              stage("S3 Build") {
                  steps {
                         //aws cloudformation create-stack --stack-name S3bucketcreation --template-body file:cft.yaml
                         aws s3api creat-bucket --bucket angular-demo-bucket --region us-east-1
                  }
              }
       }
   }
    stage ('Deploy'){
      steps{
        aws s3 cp dist/ s3://AngularS3Bucket/ --recursive --region us-east-1
      }
    }
}
