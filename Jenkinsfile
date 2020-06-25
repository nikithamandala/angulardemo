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
                         sh 'ng build'
                  }
             }
              
       }
   }
    
}
}
