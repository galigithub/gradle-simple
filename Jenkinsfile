node {
    stage('Checkout') {
        checkout scm
    }
    
    stage('Gradle Static Analysis'){
        withSonarQubeEnv('DevSecOpsSonar') {
            sh "./gradlew clean sonarqube"
        }
    }
}    
