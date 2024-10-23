#!/usr/bin/env groovy

pipeline {
    agent any
    
    tools {
            jdk 'jdk17'
            maven 'maven3'
        }

    stages {
        stage('Build') {
            steps {
                sh 'mvn clean install' 
            }
        }
        
        stage('Docker Build & Push'){
            steps {
                script {
                    withDockerRegistry(credentialsId: 'dockercred', toolName: 'docker') {
                        
                        sh "docker build -t petclinic1 ."
                        sh "docker tag petclinic1 siiyyko/my-petclinic:latest "
                        sh "docker push siiyyko/my-petclinic:latest "
                    }
                }
            }
        }
    }
}