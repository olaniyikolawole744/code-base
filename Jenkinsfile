pipeline {
    
    agent { dockerfile true }
      
      stages {    
       
        stage('Manage Build Branch') {
            when {
                branch "develop"
            }
              steps {
                
              }
        }            

            

            stage('Manage main Branch') {
            when {
                branch "main"
            }
            steps {
                echo 'main branch'
             }
         }
      }
    }