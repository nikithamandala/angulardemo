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
                         sh ' npm install '
                         sh ' npm install -g @angular/cli@8 '
                         sh ' echo Building Angular Project '
                         ng build
                  }
             }
              
       }
   }
    
}
