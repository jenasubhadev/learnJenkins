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
                      TimeMetrics.calculateStepTime('Build','Step 1 in Stage 1'){
                        sleep(time: 10, unit: 'SECONDS')
                        buildJar("Step1")
                      }
                      TimeMetrics.calculateStepTime("Build", "Step 2 in Stage 1"){
                        sleep(time: 5, unit: 'SECONDS')
                        buildJar("Step2")
                      }   
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

  TimeMetrics.stageTimes.each { stage, stage_duration ->
      reportContent += "<li>Stage '${stage}' took ${stage_duration} milliseconds</li>"
      def innerMap = TimeMetrics.stepTimes[stage]
      
      if (!innerMap.empty) {
        reportContent += """
          </ul>
          <h2>Step Times:</h2>
          <ul>
        """
        innerMap.each { step, step_duration ->
            reportContent += "<li>Step '${step}' took ${step_duration} milliseconds</li>"
        }
      }
  }

  reportContent += """
      </ul>
    </body>
    </html>
  """

  writeFile file: 'timing_report.html', text: reportContent
}
