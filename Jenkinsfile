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
            steps{
                timeout(time: 1, unit: 'HOURS'){
                   def qg = waitForQualityGate()
                   if (qg.status != 'OK'){
                      error "Pipeline aborted due to quality gate failure: ${qg.status}" 
                   }
                }

            }
        }

    }
}
