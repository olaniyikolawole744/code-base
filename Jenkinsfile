pipeline {
    agent any
    environment {
        DOCKERHUB_CREDENTIALS = credentials('DOCKERSECRET')
    }

    
       stages {    
        stage('Manage Build Branch') {
            when {
                branch "develop"
            }
            steps {
               
    
                sh 'ls && sudo docker build -t direction-dev:latest .'
                
            }
        }
            

            stage('Manage Test Branch') {
            when {
                branch "develop"
                        }
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-token', passwordVariable: '', usernameVariable: '')]) {
    // some block
    sh 'sudo docker tag direction-dev:latest olaniyikolawole744/direction-dev:latest'
                sh 'sudo docker push olaniyikolawole744/direction-dev:latest'    
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


withCredentials([usernamePassword(credentialsId: 'dockerhub-token', passwordVariable: '', usernameVariable: '')]) {
    // some block
}
    
        
    




    