pipeline {
    
    agent { dockerfile true }
      
      stages {    
       
        stage('Manage Build Branch') {
            when {
                branch "develop"
            }
              steps {
                checkout scm
                docker.withRegistry('https://hub.docker.com/r/olaniyikolawole744/direction-prod', 'docker-hub-token')
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