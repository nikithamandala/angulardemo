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
                         sh ' echo Installing packages '
                         sh ' npm install '
                         sh ' npm install -g @angular/cli@8 '
                         sh ' echo Building Angular Project '
                         sh ' ng build '
                  }
             }
             stage("S3 Build") {
                  steps {
                         withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: 'deploytos3', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]){ 
                         sh 'aws s3api create-bucket --bucket ravi-varma-devulapally-new-1-2-com --region us-east-1'
                        }
                  }
              }
       }
   }
   
    stage ('push'){
      steps{
        withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: 'deploytos3', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
        sh 'aws s3 ls'
        sh 'aws s3 ls s3://ravi-varma-devulapally-new-1-2-com'
        sh 'echo pwd'
        sh 'aws s3 docker cp ~/var/jenkins_home/workspace/awspro@2/dist/ s3://ravi-varma-devulapally-new-1-2-com/ --region us-east-1'
      } 
       }
   }
    
}
}
