#!/usr/bin/env groovy

library identifier: 'jenkins-shared-library@feature/extracting-logic-to-groovy-script', retriever: modernSCM(
    [$class: 'GitSCMSource',
     remote: 'https://github.com/himanshupant4899/Jenkins-shared-library.git',
     credentialsId: 'Github-Credentials'
    ]
)
//@Library('jenkins-shared-library') --> used when configured via UI
def gv

pipeline{
    agent any
    tools{
        maven 'maven-3.8'
    }
    stages{
        stage("init"){
            steps{
                script{
                    gv = load "script.groovy"
                }
            }
        }
        stage("build jar"){
            steps{
                script{
                    buildJar()
                }
            }
        }
        stage("build image"){
            steps{
                script{
                    buildImage 'himanshupant4899/demo-app:jma-2.0'
                    dockerLogin()
                    dockerPush 'himanshupant4899/demo-app:jma-2.0'
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