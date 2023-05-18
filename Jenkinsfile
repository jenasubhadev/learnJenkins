#!/usr/bin/env groovy 
@Library('jenkins-shared-library')_


pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                script {
                    buildJar()
                }
            }
        }
        stage('Test') {
            steps {
                echo 'Hello Test'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Hello Deploy'
            }
        }
    }
}
