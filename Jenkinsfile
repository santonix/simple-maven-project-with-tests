pipeline {
    agent {
        node {
            label 'built-in'
        }
    }
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Build') {
            steps {
                withMaven(maven: 'maven3') {
                    script {
                        sh 'mvn clean verify'
                    }
                }
            }
        }
        stage('Results') {
            steps {
                junit '**/target/surefire-reports/TEST-*.xml' // Execute tests and generate JUnit reports
                archiveArtifacts 'target/*.jar' // Archive the built JAR file
            }
        }
    }
}
