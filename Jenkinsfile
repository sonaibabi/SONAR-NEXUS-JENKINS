pipeline{
    agent any
    stage("Sonar Qube Analysis"){
            steps{
                withSonarQubeEnv('sonarserver'){
                    sh 'mvn clean sonar:sonar'
                }
                
            }
        }
    stage("Quality Gate") {
            steps {
                timeout(time: 1, unit: 'HOURS') {
                    // Parameter indicates whether to set pipeline to UNSTABLE if Quality Gate fails
                    // true = set pipeline to UNSTABLE, false = don't
                    waitForQualityGate abortPipeline: true
                }
            }
    }
}
