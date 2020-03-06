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
            if (qg.status != 'OK') {
                error "Pipeline aborted due to quality gate failure: ${qg.status}"
            } else {
                notifySonarStatus(currentBuild.currentResult)
            }
        }
    }
}    

def notifySonarStatus(String buildStatus = 'STARTED') {
   
    def mailReceipients = "shivakumargali83@gmail.com"
    def jobName = currentBuild.fullDisplayName
    
    emailext (
        subject: "Job '${env.JOB_NAME} ${env.BUILD_NUMBER}'",
        body: """<p>Check console output at <a href="${env.BUILD_URL}">${env.JOB_NAME}</a></p>""",
        to: "shivakumargali83@gmail.com",
        from: "shivakumar399@gmail.com"
    )
}
