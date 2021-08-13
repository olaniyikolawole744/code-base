pipeline {
    agent any
    environment {
        DOCKERHUB_CREDENTIALS = credentials('DOCKERTOKEN')
    }

    options { 
        disableConcurrentBuilds() 
        }

    stages {
        stage('build image') {
            steps {
                sh 'sudo docker build -t direction-dev:latest .'
                }
            }

        stage('Login to Dockerhub') {
            steps {
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
                }
            }

        stage('push to hub') {
            steps {
                sh 'ls && sudo docker push direction-dev:latest'
                }
            }

        stage('Manage Master Branch') {
            
            when {
                
                branch "main"
            }
            steps {
                echo 'main branch'
                 }
            }
            
        }

    }


