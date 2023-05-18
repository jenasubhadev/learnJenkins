#!/usr/bin/env groovy 
@Library('jenkins-shared-library')_


pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                script {
                    buildJar("Sesha")
                }
            }
        }
        stage('Test') {
            steps {
                script {
                    buildJar("Sneha")
                }
            }
        }
        stage('Deploy') {
            steps {
                echo 'Hello Deploy'
            }
        }
    }
}
