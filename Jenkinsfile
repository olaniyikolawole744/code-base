pipeline {
    
    agent { dockerfile true }
      
      stages {    
       
        stage('Manage Build Branch') {
            when {
                branch "develop"
            }
              steps {
                node {
    checkout scm

    docker.withRegistry('https://hub.docker.com/r/olaniyikolawole744/direction-prod', 'docker-hub-token') {

        def customImage = docker.build("direction-prod:latest")

        /* Push the container to the custom Registry */
        customImage.push()
    }
}          
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