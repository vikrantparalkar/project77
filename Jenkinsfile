pipeline {
    agent any

    environment{
        CONTAINER_NAME = "nestjs-app"
        IMAGE_NAME = "nestjs-image"
        EMAIL = "vikrantparalkar21@gmail.com"
        PORT = "3000"
    }

    stages{
        stage('clone repo'){
            steps{
                git branch: 'main', url: 'https://github.com/vikrantparalkar/project77'
            }
            
        }
        stage('build docker image'){
            steps{
                sh 'docker build -t $IMAGE_NAME .'
            }
        }
        stage('stop and remove previous container'){
            steps{
                sh """
                    docker stop $CONTAINER_NAME || true
                    docker rm $CONTAINER_NAME || true
                """
            }
        }
         stage('docker container run'){
            steps{
                sh """
                docker run -d -p ${PORT}:${PORT} --name $CONTAINER_NAME $IMAGE_NAME
                """
            }
        }
        stage('send email notification'){
            steps{
                emailext(
                    subject: "NestJS App Deployed Successfully on EC2!",
                    body: "Tour Nest JS App is Deployed!",
                    http://13.62.51.205:${PORT}/
                    to: "${EMAIL}"


                )
            }
        }
        
    }
}