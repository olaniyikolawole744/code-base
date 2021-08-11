pipeline {
    agent any
    environment {
        DOCKERHUB_CREDENTIALS = credentials ('dockerhub-id')
    }
    stages {
        stage('Login to Dockerhub') {
            steps {
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
                }
            }


        stage('Manage Master Branch') {
            when {
                
                branch "main"
            }
            steps {
                sh 'ls && docker build -t direction-prod:latest . \
                && docker tag direction-prod:latest olaniyikolawole744/direction-prod:latest && echo "yeeeeeeexit" && docker push olaniyikolawole744/direction-prod:latest \
                && docker pull olaniyikolawole744/direction-prod && docker run -d -p 9999:8080 -e loginname=myname -e loginpass=mypass -e api_key=*****  olaniyikolawole744/direction-prod:latest'
                }
            }


        stage('Manage Develop Branch') {
            when {
                
                branch "develop"
            }
            steps {
                sleep(time: 50, unit: "SECONDS")
                sh 'ls && docker build -t direction-dev:latest . \
                && docker tag direction-dev:latest olaniyikolawole744/direction-dev:latest && docker push olaniyikolawole744/direction-dev:latest \
                && docker pull olaniyikolawole744/direction-dev:latest && docker run -d -p 9999:8080 -e loginname=myname -e loginpass=mypass -e api_key=*****  direction-dev:latest'
                }
            }

        }
    }

