pipeline {
    agent {label 'Sonar'}
    stages{
        stage('SCM') {
            steps{
                checkout scm
            }
        }
        stage('SonarQube analysis') {
            steps{
                withSonarQubeEnv('SonarQube server') { // Will pick the global server connection you have configured
                    sh './gradlew sonar'
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
}