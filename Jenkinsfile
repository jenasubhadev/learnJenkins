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
  success {
    archiveArtifacts artifacts: 'timing_report.html', onlyIfSuccessful: true
  }
}
}

def generateTimingReport1() {
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

def generateTimingReport() {
  def reportContent = """
    <html>
    <head>
      <title>Timing Report</title>
    </head>
    <body>
      <h1>Timing Report</h1>
      <h2>Stage Times:</h2>
      <ul>
  """

  TimeMetrics.stageTimes.each { stage, duration ->
    reportContent += "<li>Stage '${stage}' took ${duration} milliseconds</li>"
  }

  reportContent += """
      </ul>
      <h2>Step Times:</h2>
      <ul>
  """

  TimeMetrics.stepTimes.each { step, duration ->
    reportContent += "<li>Step '${step}' took ${duration} milliseconds</li>"
  }

  reportContent += """
      </ul>
    </body>
    </html>
  """

  writeFile file: 'timing_report.html', text: reportContent
}
