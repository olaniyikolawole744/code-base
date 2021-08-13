pipeline {
    agent any
    environment {
        DOCKERHUB_CREDENTIALS = credentials ('docker-login')
    }

    stages {
        stage('Login to Dockerhub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'ppppp', passwordVariable: 'pass', usernameVariable: 'user')]) {
                sh 'ls && sudo docker build -t direction-prod:latest .'
                sh 'sudo docker tag direction-prod:latest olaniyikolawole744/direction-prod:latest'
                sh 'sudo docker tag direction-dev:latest olaniyikolawole744/direction-dev:latest'
                sh 'sudo docker login -u olaniyikolawole744 -p $pass'
                sh 'sudo docker push olaniyikolawole744/direction-prod:latest'
                sh 'sudo docker push olaniyikolawole744/direction-dev:latest'
            }
          }
        }

        stage('Manage Master Branch') {
            when {
              branch "main"
            }
            steps {
                withCredentials([sshUserPrivateKey(credentialsId: 'jenkins-server-key', keyFileVariable: '')]) {
                sh 'ssh ec2-user@54.162.18.130 sudo docker run -d -p 8080:8080 -e loginname=myname -e loginpass=mypass -e api_key=*****  olaniyikolawole744/direction-prod:latest'
             }
         }
    }

        stage('Manage Develop Branch') {
            when {
                branch "develop"
            }
            steps {
                withCredentials([sshUserPrivateKey(credentialsId: 'jenkins-server-key', keyFileVariable: '')]) {
                sh 'ssh ec2-user@34.229.241.39 sudo  docker run -d -p 8080:8080 -e loginname=myname -e loginpass=mypass -e api_key=*****  direction-dev:latest'
                    }
                }
            }
        }
    }

