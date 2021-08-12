pipeline {
    agent any
    
       stages {    
        stage('Manage Build Branch') {
            when {
                branch "develop"
            }
            steps {
                
                withCredentials([usernamePassword(credentialsId: 'dockerhub-token', passwordVariable: '', usernameVariable: '')]) {
                sh 'ls && sudo docker build -t direction-dev:latest .'
                }
            }
        }
            

            stage('Manage Test Branch') {
            when {
                branch "develop"
                        }
            steps {
                
                withCredentials([usernamePassword(credentialsId: 'dockerhub-token', passwordVariable: '', usernameVariable: '')]) {
                sh 'sudo docker tag direction-dev:latest olaniyikolawole744/direction-dev:latest'
                sh 'sudo docker push olaniyikolawole744/direction-dev:latest'                    
                }
             }
        }

            stage('Manage Deploy Branch') {
            when {
                branch "develop"
            }
            steps {
                withCredentials([sshUserPrivateKey(credentialsId: 'jenkins-server-key', keyFileVariable: '')]) {
                sh 'ssh ec2-user@34.229.241.39 sudo  docker run -d -p 8080:8080 -e loginname=myname -e loginpass=mypass -e api_key=*****  direction-dev:latest'
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
    
        
    




    