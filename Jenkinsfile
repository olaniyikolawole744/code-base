pipeline {
    agent any
   
    stages {
        stage('Manage Master Branch') {
           when {
                branch "main"
            }
            steps {
                withCredentials([sshUserPrivateKey(credentialsId: 'jenkins-server-key', keyFileVariable: ''),
                usernamePassword(credentialsId: 'dockerhub-token', passwordVariable: '', usernameVariable: '')])  {
                sh 'ssh ec2-user@54.162.18.130  ls && sudo docker build -t direction-prod:latest .' 
                sh 'ssh ec2-user@54.162.18.130  sudo docker tag direction-prod:latest olaniyikolawole744/direction-prod:latest'
                }
            }
       }


        stage('Manage Develop Branch') {
            when {
                branch "develop"
            }
            steps {
                
                withCredentials([sshUserPrivateKey(credentialsId: 'jenkins-server-key', keyFileVariable: ''),
                                 usernamePassword(credentialsId: 'dockerhub-token', passwordVariable: '', usernameVariable: '')]) {
                sh 'ssh ec2-user@34.229.241.39 ls && sudo docker build -t direction-dev:latest .'
                sh 'ssh ec2-user@34.229.241.39 sudo docker tag direction-dev:latest olaniyikolawole744/direction-dev:latest'
                    }
                }
            }
        }
    }




    