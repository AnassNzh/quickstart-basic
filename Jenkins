node{
    stage('SonarQube analysis'){
        def scannerHome = tool 'sonar-scanner'
        withSonarQubeEnv('SonarQube server'){
            sh "${scannerHome}/bin/sonar-scanner -X"
        }
    }
    stage("Quality Gate"){
      timeout(time: 1, unit: 'HOURS') { // Just in case something goes wrong, pipeline will be killed after a timeout
        def qg = waitForQualityGate() // Reuse taskId previously collected by withSonarQubeEnv
        if (qg.status != 'OK') {
          error "Pipeline aborted due to quality gate failure: ${qg.status}"
        }
      }
    }
}
