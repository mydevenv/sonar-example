pipeline {
    agent {
    label "ng-test-adhoc"
  }
    stages {
        stage('SCM') {
            steps {
                git url: 'https://github.com/mydevenv/sonar-example.git'
            }
        }
        stage('build && SonarQube analysis') {
            steps {
                withSonarQubeEnv('SonarCloud') {
                  sh "${SONAR_SCANNER_HOME}/bin/sonar-scanner"  
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