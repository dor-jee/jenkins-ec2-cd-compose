#!/usr/bin.env groovy

pipeline {   
    agent any
    stages {
        stage("test") {
            steps {
                script {
                    echo "Testing the application..."

                }
            }
        }
        stage("build") {
            steps {
                script {
                    echo "Building the application..."
                }
            }
        }

        stage("deploy") {
            steps {
                script {
                    echo "deploying to EC2 "
                    def dockerCmd = "docker compose -f docker-compose.yaml up -d"
                    sshagent(credentials: ['ec2-key']) {
                        sh "scp docker-compose.yaml ec2-user@51.96.20.64:/home/ec2-user"
                        sh "ssh -o StrictHostKeyChecking=no ec2-user@51.96.20.64 ${dockerCmd}"
                    }
                }
            }
        }               
    }
} 
