#!/usr/bin/env groovy
def gv

pipeline{
    agent any
    parameters{
        choice(name: 'VERSION', choices: ['1.1.0','1.2.0','1.3.0'],description: '')
        booleanParam(name: 'executeTests', defaultValue: true, description: '')
    }
    stages{
        stage("init"){
            script{
                gv = load "script.groovy"
            }
        }
        stage("build"){
            gv.buildApp()
        }
        stage("test"){
            gv.testApp()
        }
        stage("deploy"){
            gv.deployApp()
        }
    }
}