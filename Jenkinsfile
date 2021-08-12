pipeline {
    agent any
   
    stages {
        
        stage('Manage Master Branch') {
           when {
                branch "main"
            }
            steps {
                withCredentials([
                usernamePassword(credentialsId: 'dockerhub-token', passwordVariable: '', usernameVariable: '')])  {
                lock('master') { sh 'ls && sudo docker build -t direction-prod:latest .' }
                sh 'sudo docker tag direction-prod:latest olaniyikolawole744/direction-prod:latest'
                sh 'sudo docker push olaniyikolawole744/direction-prod:latest'
                }

                withCredentials([sshUserPrivateKey(credentialsId: 'jenkins-server-key', keyFileVariable: '')
                ])  {
                sh 'ssh ec2-user@54.162.18.130 sudo docker run -d -p 8080:8080 -e loginname=myname -e loginpass=mypass -e api_key=*****  olaniyikolawole744/direction-prod:latest'
                }
                }
            }
       

        
        stage('Manage Develop Branch') {
            when {
                branch "develop"
            }
            steps {
                
                withCredentials([
                                 usernamePassword(credentialsId: 'dockerhub-token', passwordVariable: '', usernameVariable: '')]) {
                lock('develop') {   sh 'ssh ec2-user@34.229.241.39 ls && sudo docker build -t direction-dev:latest .'}
                sh 'ssh ec2-user@34.229.241.39 sudo docker tag direction-dev:latest olaniyikolawole744/direction-dev:latest'
                sh 'sudo docker push olaniyikolawole744/direction-dev:latest'                    
                                     }

                withCredentials([sshUserPrivateKey(credentialsId: 'jenkins-server-key', keyFileVariable: '')
                                 ]) {
                sh 'ssh ec2-user@34.229.241.39 sudo  docker run -d -p 8080:8080 -e loginname=myname -e loginpass=mypass -e api_key=*****  direction-dev:latest'
                   

                }

                }
            }
    
        
    




    