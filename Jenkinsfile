pipeline{
    agent any
    stages{
        stage("Git Checkout"){
            steps{
                git credentialsId: 'GitPass', url: 'https://github.com/sonaibabi/SONAR-NEXUS-JENKINS.git'
            }
            
        }
        stage("Sonar Qube Analysis"){
            steps{
                withSonarQubeEnv('sonarserver'){
                    sh 'mvn clean sonar:sonar'
                }
                
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
}
