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
                TimeMetrics.calculateStageTime("Test")
            }
        }
        stage('Deploy') {
            steps {
                echo 'Hello Deploy'
            }
        }
    }
  post {
    always {
      script {
        generateTimingReport()
      }
    }
  }
}
