pipeline{
    agent any
    stages{
        stage("SonarQube analysis"){
            environment {
                scannerHome = tool 'sonar-scanner'
            }
            steps{
                withSonarQubeEnv('SonarQube server'){
                    sh "${scannerHome}/bin/sonar-scanner -X"
                }
                timeout(time: 10, unit: 'MINUTES') {
                    waitForQualityGate abortPipeline: true
                }
            }

        }
    }
}
