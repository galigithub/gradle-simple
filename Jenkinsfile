node {
    stage('Checkout') {
        checkout scm
    }
    
    stage('Gradle Static Analysis'){
        withSonarQubeEnv('DevSecOpsSonar') {
            sh "./gradlew clean sonarqube"
        }
    }
    
    stage('Quality Gates'){
        timeout(time: 1, unit: 'HOURS') {
            def qg = waitForQualityGate()
            if (qg.status == 'OK') {
                error "Pipeline aborted due to quality gate failure: ${qg.status}"
            }
        }
    }
}    
