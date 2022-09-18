#!/usr/bin/env groovy
def gv

pipeline{
    agent any
    tools{
        maven 'maven-3.8'
    }
    stages{
        stage("build jar"){
            steps{
                script{
                    echo "Building the application"
                    sh 'mvn package'
                }
            }
        }
        stage("build image"){
            steps{
                script{
                    echo "Building the docker image"
                    withCredentials([usernamePassword(credentialsId: 'docker-hub-repo',passwordVariable: 'PASS',usernameVariable: 'USER')]){
                        sh 'docker build -t himanshupant4899/demo-app:jma-1.0 .'
                        sh "echo $PASS | docker login -u $USER --password-stdin"
                        sh 'docker push himanshupant4899/demo-app:jma-1.0'
                    }
                }
            }
        }
        stage("test"){
            when{
                expression{
                    params.executeTests
                }
            }
            steps{
                script{
                    gv.testApp()
                }
            }
        }
        stage("deploy"){
            steps{
                script{
                    gv.deployApp()
                }
            }
        }
    }
}