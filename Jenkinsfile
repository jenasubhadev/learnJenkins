#!/usr/bin/env groovy 
@Library('jenkins-shared-library')
import org.example.TimeMetrics

pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                script {
                    TimeMetrics.calculateStageTime("Build"){
                        buildJar("SeshaAgain")
                    }
                    
                }
            }
        }
        stage('Test') {
            steps {
                script {
                    TimeMetrics.calculateStageTime("Test"){
                        buildJar("SnehaAgain")
                    }
                }
            }
        }
        stage('Deploy') {
            steps {
                script {
                    TimeMetrics.calculateStageTime("Deploy"){
                        buildJar("DeployAgain")
                    }
                }
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

def generateTimingReport() {
  println "----- Timing Report -----"
  println "Stage Times:"
  TimeMetrics.stageTimes.each { stage, duration ->
    println "Stage '${stage}' took ${duration} milliseconds"
  }
  println "Step Times:"
  TimeMetrics.stepTimes.each { step, duration ->
    println "Step '${step}' took ${duration} milliseconds"
  }
  println "-------------------------"
}