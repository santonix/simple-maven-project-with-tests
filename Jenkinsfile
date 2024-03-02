node ('built-in') {
    checkout scm // Checkout the source code

    stage('Build') {
        withMaven(maven: 'M3') {
            if (isUnix()) {
                sh 'mvn -Dmaven.test.failure.ignore clean package' // Execute Maven build (Unix)
            } else {
                bat 'mvn -Dmaven.test.failure.ignore clean package' // Execute Maven build (Windows)
            }
        }
    }

    stage('Results') {
        junit '**/target/surefire-reports/TEST-*.xml' // Execute tests and generate JUnit reports
        archive 'target/*.jar' // Archive the built JAR file
    }
}
