pipeline {
      agent any
      environment {
           SG_CLIENT_ID = credentials("SG_CLIENT_ID")
           SG_SECRET_KEY = credentials("SG_SECRET_KEY")
           registry = "https://registry.hub.docker.com"
       
           dockerImage = 'dhouari/sg'
        }
  stages {
          
         stage('Clone Github repository') {
            
    
           steps {
              
             checkout scm
           
             }
  
          }
   
          stage('Docker image Build and scan prep') {
             
            steps {

              sh 'docker build -t dhouari/sg .'
             
              
             } 
           }
       
            
        stage('Publish') {
          environment {
               registryCredential = 'dockerhub'
            }
           steps{
               script {
                   def appimage = "dhouari/sg"
                   docker.withRegistry( '', registryCredential ) {
                       appimage.push()
                       appimage.push('latest')
                   }
               }
           }
       }
        
  } 
}
