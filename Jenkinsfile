pipeline {
    
    agent { dockerfile true }
      
      stages {    
       
        stage('Manage Build Branch') {
            when {
                branch "develop"
            }
              steps {
                sh 'node --version'
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